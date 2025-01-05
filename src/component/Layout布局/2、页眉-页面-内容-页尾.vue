<template>
	<!-- 定义了一个包含布局组件的div容器 -->
	<div class="layout-demo">
		<!-- 
        a-layout组件用于创建一个布局结构，通过设置高度宽度百分比限制整个布局的高度。
        内部包含了三个子组件：Header、Content和Footer。
        -->
		<a-layout style="height: 50vh; width: 100vh">
			<a-layout-header>页眉</a-layout-header>
			<a-layout>
				<a-layout-sider>页面</a-layout-sider>
				<a-layout-content>内容</a-layout-content>
			</a-layout>
			<a-layout-footer>页尾</a-layout-footer>
		</a-layout>
	</div>
</template>
<style scoped>
	/* 使用 :deep() 深度选择器来覆盖 Arco Design 组件内部元素的样式 */
	.layout-demo :deep(.arco-layout-header),
	.layout-demo :deep(.arco-layout-footer),
	.layout-demo :deep(.arco-layout-sider-children),
	.layout-demo :deep(.arco-layout-content) {
		/* 使用Flexbox布局使内容垂直居中 */
		display: flex;
		flex-direction: column;
		justify-content: center;

		/* 设置文本颜色、字体大小、字体拉伸方式和文本对齐方式 */
		color: var(--color-white); /* 文本颜色为白色 */
		font-size: 16px; /* 字体大小为16像素 */
		font-stretch: condensed; /* 字体拉伸为紧凑型 */
		text-align: center; /* 文本居中对齐 */
	}

	/* Header 和 Footer 样式 */
	.layout-demo :deep(.arco-layout-header),
	.layout-demo :deep(.arco-layout-footer) {
		height: 5vh; /* 高度为5% */
		background-color: var(--color-primary-light-4); /* 背景颜色使用稍微深一点的主题变量 */
	}

	/* Side Bar 样式  */
	.layout-demo :deep(.arco-layout-sider) {
		width: 20vh; /* 宽度为20% */
		background-color: var(--color-primary-light-3); /* 背景颜色使用特定的蓝色调 */
	}

	/* 背景颜色使用稍微深一点的主题变量 */
	.layout-demo :deep(.arco-layout-content) {
		background-color: rgb(var(--arcoblue-6)); /* 背景颜色使用特定的蓝色调 */
	}
</style>
