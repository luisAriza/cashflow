<template>
	<div>
		<svg viewbox="0.0 300 200">
			<line stroke="#c4c4c4" stroke-width="2" x1="0" y1="75" x2="300" y2="75" />
			<polyline
				fill="none"
				stroke="#0689b0"
				stroke-width="2"
				:points="points"
			/>
			<line
				stroke="#04b500"
				stroke-width="2"
				x1="200"
				y1="0"
				x2="200"
				y2="150"
			/>
		</svg>
		<p>Últimos 30 días</p>
	</div>
</template>

<script setup lang="ts">
	import { defineProps, toRefs, computed } from "vue";

	const props = defineProps({
		amounts: {
			type: Array,
			default: (): [] => [],
		},
	});
	const { amounts } = toRefs(props);

	const amountToPixels = () => {
		const min = Math.min(...amounts.value);
		const max = Math.max(...amounts.value);

		return `${min}, ${max}`;
	};
	const points = computed(() => {
		const total = amounts.value.length;
		return Array(total)
			.fill(75)
			.reduce((points, amounts, index): string => {
				const x = (300 / total) * (index + 1);
				const y = amountToPixels();
				console.log(y);

				return `${points} ${x},${y}`;
			}, "0, 75");
	});
</script>

<style scoped lang="scss">
	svg {
		width: 100%;
	}
	p {
		text-align: center;
	}
</style>
