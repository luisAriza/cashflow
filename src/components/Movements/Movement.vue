<template>
	<div class="movement">
		<div class="content">
			<h4>{{ title }}</h4>
			<p>{{ description }}</p>
		</div>
		<div class="action">
			<TrashIcon class="icon" @click="remove" />
			<p
				:class="{
					red: isNegative,
					green: !isNegative,
				}"
			>
				{{ amountCurrency }}
			</p>
		</div>
	</div>
</template>

<script setup lang="ts">
	import { TrashIcon } from "@heroicons/vue/24/solid";
	import { defineProps, toRefs, computed, defineEmits } from "vue";

	const props = defineProps({
		id: {
			type: Number,
			required: true,
		},
		title: {
			type: String,
			required: true,
		},
		description: {
			type: String,
			required: true,
		},
		amount: {
			type: Number,
			required: true,
		},
	});
	const { id, title, description, amount } = toRefs(props);

	const currencyFormatter = new Intl.NumberFormat("es-CO", {
		style: "currency",
		currency: "COP",
	});
	const amountCurrency = computed((): string =>
		currencyFormatter.format(amount.value)
	);
	const isNegative = computed((): boolean => amount.value <= 0);

	const emit = defineEmits(["remove"]);
	const remove = (): void => {
		emit("remove", id.value);
	};
</script>

<style scoped lang="scss">
	.movement {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		padding: 16px;
		background-color: #e6f9ff;
		border-radius: 8px;
		box-sizing: border-box;
	}
	.movement .content {
		width: 100%;
	}
	.movement .action {
		display: flex;
		justify-content: space-between;
		align-items: flex-end;
		flex-direction: column;
	}
	h4,
	p {
		margin: 0;
		padding: 0;
	}
	h4 {
		margin-bottom: 8px;
	}
	.icon {
		width: 24px;
		height: 24px;
		margin-bottom: 16px;
		color: var(--brand-blue);
	}
	.red {
		color: red;
	}
	.green {
		color: green;
	}
</style>
