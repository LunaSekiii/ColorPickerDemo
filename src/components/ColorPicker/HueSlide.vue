<script setup>
import { ref, reactive, defineEmits } from "vue";

const thumb = ref();

const thumbTop = ref(0);

const startY = ref(0);
const startTop = ref(0);

const colorHue = reactive([255, 0, 0]);
const emits = defineEmits(["hueChange"]);

const mouseMoveHandler = (e) => {
	thumbTopHandler(e.clientY - startY.value);
};

const thumbTopHandler = (relativeY) => {
	let computedTop = relativeY + startTop.value;
	if (computedTop < 0) computedTop = 0;
	else if (computedTop > 300) computedTop = 300;
	thumbTop.value = computedTop;
	colorHandlerBySlide(computedTop);
};

const colorHandlerBySlide = (slideTop) => {
	// 按照300px的slider高度，将色相划分成6个区域，每个区域各占50px

	let part = Math.floor(slideTop / 100);
	const hueInfo = Math.floor(256 * ((slideTop % 50) / 50));

	// 奇数区域颜色随高度上升
	if (!(Math.floor(slideTop / 50) % 2)) {
		if (part > 2) part = 0;
		colorHue[part] = 255;
		if (++part > 2) part = 0;
		colorHue[part] = hueInfo;
		if (++part > 2) part = 0;
		colorHue[part] = 0;
	}
	// 偶数区域颜色随高度下降
	else {
		if (part > 2) part = 0;
		colorHue[part] = 255 - hueInfo;
		if (++part > 2) part = 0;
		colorHue[part] = 255;
		if (++part > 2) part = 0;
		colorHue[part] = 0;
	}

	emits("hueChange", colorHue);
};

const mouseUpHandler = (e) => {
	console.log("end drag", e);

	window.removeEventListener("mousemove", mouseMoveHandler);
	window.removeEventListener("mouseup", mouseUpHandler);
};

function dragHandler(e) {
	startY.value = e.clientY;
	startTop.value = thumbTop.value;
	window.addEventListener("mousemove", mouseMoveHandler);
	window.addEventListener("mouseup", mouseUpHandler);
}
</script>

<template>
	<div class="hue-slide">
		<div class="hue-slide-bar" />
		<div
			class="hue-slide-thumb"
			draggable="false"
			ref="thumb"
			:style="{
				top: `${thumbTop}px`,
			}"
			@mousedown="
				(e) => {
					dragHandler(e);
					console.log('start drag', e);
				}
			"
		/>
	</div>
</template>

<style scoped>
.hue-slide {
	width: 50px;
	height: 310px;
	position: relative;
	transform: translateY(-10px);
}
.hue-slide-bar {
	width: 50px;
	height: 300px;
	margin-top: 10px;
	background: linear-gradient(
		180deg,
		red 0,
		#ff0 17%,
		#0f0 33%,
		#0ff 50%,
		#00f 67%,
		#f0f 83%,
		red
	);
}
.hue-slide-thumb {
	width: 40px;
	height: 10px;
	/* background-color: #fff; */
	border: rgb(85, 85, 85) solid 5px;
	border-radius: 3px;
	position: absolute;
	cursor: pointer;
	user-select: none;
}
</style>
