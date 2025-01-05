<template>
	<!-- 定义了一个包含菜单的div容器 -->
	<div class="menu-demo">
		<!-- a-menu组件用于创建一个水平（horizontal）菜单，通过默认选中的键值（default-selected-keys）来设置初始激活项 -->
		<a-menu mode="horizontal" :default-selected-keys="['1']" style="width: 100vh">
			<!-- 
                a-menu-item组件表示菜单中的每一个项目。
                第一项（key="0"）被禁用（disabled），并且设置了自定义样式，包括宽度、高度、圆角、背景颜色和鼠标指针样式。
                此项可能作为一个占位符或装饰元素。
            -->
			<a-menu-item key="0" disabled></a-menu-item>
			<!-- 菜单项，代表首页链接 -->
			<a-menu-item key="1">首页</a-menu-item>
			<!-- 菜单项，代表解决方案链接 -->
			<a-menu-item key="2">解决方案</a-menu-item>
			<!-- 菜单项，代表云服务链接 -->
			<a-menu-item key="3">云服务</a-menu-item>
			<!-- 菜单项，代表合作链接 -->
			<a-menu-item key="4">合作</a-menu-item>
		</a-menu>
	</div>
</template>

<style scoped>
	.menu-demo {
		box-sizing: border-box;
		width: 100%;
		padding: 40px;
		background-color: var(--color-neutral-2);
	}
</style>
