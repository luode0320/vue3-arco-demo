<template>
	<a-layout class="container">
		<a-layout-sider width="20vh" style="background: #fff">
			<a-menu style="height: 100%; width: 100%" showCollapseButton>
				<template v-for="item in menuStructure" :key="item.key">
					<a-sub-menu v-if="item.children" :key="item.key" :title="item.title">
						<template v-for="subItem in item.children" :key="subItem.key">
							<a-sub-menu v-if="subItem.children" :key="subItem.key" :title="subItem.title">
								<a-menu-item v-for="child in subItem.children" :key="child.key" @click="loadDemo(child.key)">
									{{ child.title }}
								</a-menu-item>
							</a-sub-menu>
							<a-menu-item v-else :key="subItem.loader" @click="loadDemo(subItem.key)">
								{{ subItem.title }}
							</a-menu-item>
						</template>
					</a-sub-menu>
					<a-menu-item v-else :key="item.loader" @click="loadDemo(item.key)">
						{{ item.title }}
					</a-menu-item>
				</template>
			</a-menu>
		</a-layout-sider>
		<a-layout-content style="padding: 0 16px; background: #fff">
			<a-spin :loading="loading">
				<component :is="currentComponent" v-if="currentComponent" />
			</a-spin>
		</a-layout-content>
	</a-layout>
</template>

<script setup>
	import { ref, markRaw, onMounted } from 'vue';
	import { Layout, Menu, Spin } from '@arco-design/web-vue';

	const { Header, Sider, Content } = Layout;
	const { Item: MenuItem, SubMenu } = Menu;

	// 使用 import.meta.glob 动态导入所有 .vue 文件，包括子目录
	const componentFiles = import.meta.glob('./component/**/*.vue');
	const currentComponent = ref(null);
	const loading = ref(false);
	const menuStructure = ref([]);

	// 解析文件路径并构建多层级菜单结构
	function buildMenuStructure(files) {
		const structure = {};

		Object.keys(files).forEach((file) => {
			const pathParts = file.match(/\.\/component\/(.*)\.vue$/)[1].split('/');
			let currentLevel = structure;

			pathParts.forEach((part, index) => {
				// 如果是最后一个部分，则认为是组件文件
				if (index === pathParts.length - 1) {
					currentLevel[part] = {
						name: part.replace('.vue', ''),
						loader: files[file],
					};
				} else {
					// 否则，创建或进入下一层级
					if (!currentLevel[part]) {
						currentLevel[part] = {};
					}
					currentLevel = currentLevel[part];
				}
			});
		});

		return flattenMenu(structure);
	}

	// 将嵌套的对象结构转换为扁平的菜单数组
	function flattenMenu(obj, parentKey = '') {
		return Object.keys(obj).reduce((acc, key) => {
			const fullPath = parentKey ? `${parentKey}/${key}` : key;
			const value = obj[key];
			if (typeof value === 'object' && !Array.isArray(value) && value !== null && !value.name && !value.loader) {
				acc.push({
					key: fullPath,
					title: key,
					children: flattenMenu(value, fullPath),
				});
			} else {
				acc.push({
					key: fullPath,
					title: key,
					loader: value.loader,
				});
			}

			return acc;
		}, []);
	}

	onMounted(async () => {
		// 构建多层级菜单结构
		menuStructure.value = buildMenuStructure(componentFiles);
		console.log('构建多层级菜单结构:', menuStructure.value);
	});

	const loadDemo = async (fullPath) => {
		try {
			loading.value = true;
			const component = await /* @vite-ignore */ import('./component/' + fullPath + '.vue');
			currentComponent.value = markRaw(component.default);
		} catch (error) {
			console.error(`Failed to load ${fullPath}:`, error);
		} finally {
			loading.value = false;
		}
	};
</script>

<style scoped>
	.container {
		/* 按照弹性盒子模型（Flexbox）进行排列 */
		display: flex;
		height: 99vh;
	}

	/* 可选：调整 sider 样式 */
	.arco-layout-sider {
		/* 如果内容超出了容器的边界，浏览器会在需要时显示滚动条 */
		overflow: auto;
	}
</style>
