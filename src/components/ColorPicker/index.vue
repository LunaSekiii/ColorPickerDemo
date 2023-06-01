<script setup>
import PickerPanel from "./PickerPanel.vue";
import HueSlide from "./HueSlide.vue";
import { reactive } from "vue";

const colorHue = reactive([255, 0, 0]);

const hueChange = (hueColor) => {
	Object.assign(colorHue, hueColor);
};
</script>

<template>
	<div class="color-picker">
		<div class="color-picker-title">颜色面板</div>
		<div class="color-picker-main">
			<PickerPanel :colorHue="colorHue" />
			<HueSlide @hueChange="hueChange" />
		</div>
		<div>颜色：rgb({{ colorHue.join(", ") }})</div>
	</div>
</template>

<style scoped>
.color-picker {
	max-width: 600px;
	height: 400px;
	border: 1px solid var(--border-color);
	box-shadow: var(--box-shadow);
	padding: 10px;
}
.color-picker-title {
	font-size: x-large;
}

.color-picker-main {
	width: 580px;
	height: 300px;
	display: flex;
	justify-content: space-between;
}
</style>
