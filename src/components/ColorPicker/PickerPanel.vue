<script setup lang="ts">
import { defineProps } from "vue";
const posps = defineProps<{ colorHue: Array<number> }>();
</script>

<template>
	<div
		class="color-picker-panel"
		:style="{
			backgroundColor: `rgb(${colorHue.join(', ')})`,
		}"
	>
		<div class="color-picker-white" />
		<div class="color-picker-black" />
	</div>
</template>

<style scoped>
.color-picker-panel {
	width: 500px;
	height: 300px;
	display: block;
	position: relative;
}
.color-picker-white {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: linear-gradient(90deg, #fff, hsla(0, 0%, 100%, 0));
}
.color-picker-black {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	background: linear-gradient(0deg, #000, transparent);
}
</style>
