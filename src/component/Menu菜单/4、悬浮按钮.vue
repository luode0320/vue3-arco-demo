<template>
	<!-- 定义了一个包含两个触发器菜单的div容器 -->
	<div class="menu-demo">
		<!-- 
        a-trigger组件用于创建一个弹出式菜单，通过点击或悬停来触发。
        clickToClose属性确保在点击外部时关闭弹出菜单。
        position设置弹出位置为顶部（top），v-model:popupVisible绑定到popupVisible1控制第一个触发器的可见性。
        -->
		<a-trigger :trigger="['click', 'hover']" clickToClose position="top" v-model:popupVisible="popupVisible1">
			<!-- 触发按钮，根据popupVisible1的状态切换图标 -->
			<div :class="`button-trigger ${popupVisible1 ? 'button-trigger-active' : ''}`">
				<IconClose v-if="popupVisible1" />
				<IconMessage v-else />
			</div>

			<!-- 弹出内容：包含菜单项的a-menu -->
			<template #content>
				<a-menu :style="{ marginBottom: '-4px' }" mode="popButton" :tooltipProps="{ position: 'left' }" showCollapseButton>
					<a-menu-item key="1">
						<template #icon><IconBug></IconBug></template>
						Bugs
					</a-menu-item>
					<a-menu-item key="2">
						<template #icon><IconBulb></IconBulb></template>
						Ideas
					</a-menu-item>
				</a-menu>
			</template>
		</a-trigger>

		<!-- 第二个触发器，与第一个类似，但使用popupVisible2控制其可见性 -->
		<a-trigger :trigger="['click', 'hover']" clickToClose position="top" v-model:popupVisible="popupVisible2">
			<div :class="`button-trigger ${popupVisible2 ? 'button-trigger-active' : ''}`">
				<IconClose v-if="popupVisible2" />
				<IconMessage v-else />
			</div>
			<template #content>
				<a-menu :style="{ marginBottom: '-4px' }" mode="popButton" :tooltipProps="{ position: 'left' }" showCollapseButton>
					<a-menu-item key="1">
						<template #icon><IconBug></IconBug></template>
						Bugs
					</a-menu-item>
					<a-menu-item key="2">
						<template #icon><IconBulb></IconBulb></template>
						Ideas
					</a-menu-item>
				</a-menu>
			</template>
		</a-trigger>
	</div>
</template>

<script setup>
	// 使用<script setup>语法，直接引入需要的模块，并定义响应式的变量
	import { ref } from 'vue';
	import { IconBug, IconBulb, IconClose, IconMessage } from '@arco-design/web-vue/es/icon';

	// 使用ref创建两个响应式的布尔变量，用于控制两个触发器的可见性
	const popupVisible1 = ref(false);
	const popupVisible2 = ref(false);

	// 注册所有用到的图标组件，<script setup>会自动将导入的组件注册为局部组件
</script>

<style scoped>
	/* 
    设置.menu-demo类的样式，包括盒模型行为（box-sizing）、宽度、高度、内边距（padding）和背景颜色。
    */
	.menu-demo {
		box-sizing: border-box;
		width: 660px;
		height: 300px;
		padding: 40px;
		background-color: var(--color-fill-2); /* 使用CSS变量作为背景色 */
		position: relative; /* 使子元素能够相对于此容器定位 */
	}

	.button-trigger {
		position: absolute; /* 绝对定位，相对于最近的非static父级元素 */
		bottom: 80px; /* 距离底部的距离 */
		display: flex;
		align-items: center;
		justify-content: center;
		width: 40px;
		height: 40px;
		color: var(--color-white); /* 图标颜色 */
		font-size: 14px;
		border-radius: 50%; /* 圆形按钮 */
		cursor: pointer; /* 指针样式 */
		transition: all 0.1s; /* 过渡效果 */
	}

	/* 左侧触发按钮的样式 */
	.button-trigger:nth-child(1) {
		left: 150px; /* 距离左侧的距离 */
		background-color: var(--color-neutral-5); /* 默认背景色 */
	}
	.button-trigger:nth-child(1).button-trigger-active {
		background-color: var(--color-neutral-4); /* 激活状态下的背景色 */
	}

	/* 右侧触发按钮的样式 */
	.button-trigger:nth-child(2) {
		left: 372px; /* 距离左侧的距离 */
		background-color: rgb(var(--arcoblue-6)); /* 默认背景色 */
	}
	.button-trigger:nth-child(2).button-trigger-active {
		background-color: var(--color-primary-light-4); /* 激活状态下的背景色 */
	}
</style>
