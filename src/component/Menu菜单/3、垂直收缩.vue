<template>
	<!-- 定义了一个包含菜单的div容器 -->
	<div class="menu-demo">
		<!--
        a-menu组件用于创建一个垂直（默认）菜单，设置了宽度、高度、默认打开的子菜单键值（default-open-keys）、默认选中的菜单项键值（default-selected-keys）。
        showCollapseButton属性显示折叠按钮，breakpoint设置响应式断点为超大屏幕（xl），@collapse事件监听器绑定到onCollapse方法上。
        -->
		<a-menu :style="{ width: '100%', height: '100%' }" :default-open-keys="['0']" :default-selected-keys="['0_2']" showCollapseButton breakpoint="xl" @collapse="onCollapse">
			<!-- a-sub-menu组件表示菜单中的子菜单，可以包含多个a-menu-item。 -->
			<a-sub-menu key="0">
				<!-- #icon插槽用于定义子菜单前的图标 -->
				<template #icon><icon-apps></icon-apps></template>
				<!-- #icon插槽用于定义子菜单前的图标 -->
				<template #title>导航 1</template>
				<!-- a-menu-item组件代表子菜单下的每个菜单项 -->
				<a-menu-item key="0_0">菜单 1</a-menu-item>
				<a-menu-item key="0_1">菜单 2</a-menu-item>
				<a-menu-item key="0_2">菜单 3</a-menu-item>
				<a-menu-item key="0_3">菜单 4</a-menu-item>
			</a-sub-menu>

			<a-sub-menu key="1">
				<template #icon><icon-bug></icon-bug></template>
				<template #title>导航 2</template>
				<a-menu-item key="1_0">菜单 1</a-menu-item>
				<a-menu-item key="1_1">菜单 2</a-menu-item>
				<a-menu-item key="1_2">菜单 3</a-menu-item>
			</a-sub-menu>

			<a-sub-menu key="2">
				<template #icon><icon-bulb></icon-bulb></template>
				<template #title>导航 3</template>
				<a-menu-item key="2_0">菜单 1</a-menu-item>
				<a-menu-item key="2_1">菜单 2</a-menu-item>
				<a-sub-menu key="2_2" title="导航 4">
					<a-menu-item key="2_2_0">菜单 1</a-menu-item>
					<a-menu-item key="2_2_1">菜单 2</a-menu-item>
				</a-sub-menu>
			</a-sub-menu>
		</a-menu>
	</div>
</template>

<script setup>
	// 引入Vue的ref函数和Message组件，以及所需的所有图标组件
	import { ref, defineEmits } from 'vue';
	import { Message } from '@arco-design/web-vue';
	import '@arco-design/web-vue/es/icon';

	// 定义onCollapse方法，用于处理菜单折叠或展开时触发的事件
	const emit = defineEmits(['collapse']);
	const onCollapse = (val, type) => {
		// 根据触发类型（响应式或点击）显示不同的信息提示
		const content = type === 'responsive' ? '触发响应式收缩' : '点击触发收缩';
		Message.info({
			content,
			duration: 2000, // 消息持续时间，单位毫秒
		});
	};

	// 注册所有用到的图标组件，<script setup>会自动将导入的组件注册为局部组件
</script>

<style scoped>
	/* 
    设置.menu-demo类的样式，包括盒模型行为（box-sizing）、宽度、高度、内边距（padding）和背景颜色。
    */
	.menu-demo {
		box-sizing: border-box;
		width: 20vh;
		height: 99vh;
		background-color: var(--color-neutral-2); /* 使用CSS变量作为背景色 */
	}
</style>
