<template>
	<main>
		<p>{{ labelVisual }}</p>
		<h1>{{ amountCurrency }}</h1>
		<div class="graphic">
			<slot name="graphic"></slot>
		</div>
		<div class="action">
			<slot name="action"></slot>
		</div>
	</main>
</template>

<script setup lang="ts">
	import { defineProps, toRefs, computed } from "vue";

	const props = defineProps({
		totalLabel: {
			type: String,
			required: true,
		},
		label: {
			type: String,
			default: null,
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
	const { totalLabel, label, totalAmount, amount } = toRefs(props);

	const labelVisual = computed((): string => label.value !== null ? label.value : totalLabel.value);
	const amountVisual = computed((): number => amount.value !== null ? amount.value : totalAmount.value);

	const currencyFormatter = new Intl.NumberFormat("es-CO", {
		style: "currency",
		currency: "COP",
	});
	const amountCurrency = computed((): string =>
		currencyFormatter.format(amountVisual.value)
	);
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
