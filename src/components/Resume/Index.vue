<template>
	<main>
		<p>{{ label }}</p>
		<h1>{{ amountVisual }}</h1>
	</main>
</template>

<script setup lang="ts">
	import { defineProps, toRefs, computed, Ref } from "vue";

	const props = defineProps({
		label: {
			type: String,
			required: true,
		},
		totalAmount: {
			type: Number,
			required: true,
		},
		amount: {
			type: Number,
			default: null,
		},
	});
	const { label, totalAmount, amount } = toRefs(props);

	const amountVisual = computed((): Ref<number> => {
		return amount.value !== null ? amount : totalAmount;
	});

	console.log(amountVisual);
</script>

<style scoped lang="scss">
	main {
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		width: 100%;
	}
	h1,
	p {
		margin: 0;
		text-align: center;
	}
	h1 {
		margin-top: 14px;
		color: var(--brand-green);
	}
	.graphic {
		display: flex;
		justify-content: center;
		align-items: center;
		width: 100%;
		padding: 48px 24px;
		box-sizing: border-box;
	}
</style>
