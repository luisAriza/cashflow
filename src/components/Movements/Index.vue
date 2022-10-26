<template>
	<div class="movements">
		<h2 class="title">Historial</h2>
		<div class="content">
			<Movement
				v-for="{ id, title, description, amount } in movements"
				:key="id"
				:id="id"
				:title="title"
				:description="description"
				:amount="amount"
				@remove="remove"
			/>
		</div>
	</div>
</template>

<script setup lang="ts">
	import { defineProps, toRefs } from "vue";
	import Movement from "./Movement.vue";

	type Movements = {
		id: number;
		title: string;
		description: string;
		amount: number;
	};
	type Props = {
		movements: Movements[];
	};

	const props = defineProps({
		movements: {
			type: Array,
			default: (): [] => [],
			required: true,
		},
	});
	const { movements }: Props = toRefs(props);

	const remove = (id: number): void => {
		console.log("remove", id);
	};
</script>

<style scoped lang="scss">
	.movements {
		max-height: 100%;
		padding: 0 8px;
		margin-bottom: 14px;
	}
	.title {
		margin: 8px 16px 24px 16px;
		color: var(--brand-blue);
	}
	.content {
		max-height: 68vh;
		display: flex;
		flex-direction: column;
		gap: 8px;
		overflow-y: scroll;
	}
</style>
