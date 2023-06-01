<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import ColorPicker from "./components/ColorPicker/index.vue";
</script>

<template>
	<div class="main">
		<ColorPicker />
	</div>
</template>

<style scoped>
.main {
	width: 100vw;
	height: 100vh;
	display: flex;
	justify-content: center;
	align-items: center;
	background-color: #fff;
}
</style>
