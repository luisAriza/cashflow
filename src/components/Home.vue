<template>
	<Layout>
		<template #header>
			<Header />
		</template>
		<template #resume>
			<Resume :total-label="'Ahorro total'" :label="label"  :total-amount="totalAmount" :amount="amount">
				<template #graphic>
					<Graphic :amounts="amounts" @select="select"/>
				</template>
				<template #action>
					<Action @create="create" />
				</template>
			</Resume>
		</template>
		<template #movements>
			<Movements :movements="movements" @remove="remove" />
		</template>
	</Layout>
</template>

<script lang="ts" setup>
	import Layout from "./Layout.vue";
	import Header from "./Header.vue";
	import Resume from "./Resume/Index.vue";
	import Graphic from "./Resume/Graphic.vue";
	import Action from "./Action.vue";
	import Movements from "./Movements/Index.vue";
	import { ref, computed, onMounted, Ref } from "vue";

	type Movements = {
		id: number;
		title: string;
		description: string;
		amount: number;
		time: number | Date;
	};

	const amount  = ref(null);
	const label = ref(null);
	const movements: any = ref([]);

	const amounts = computed(() => {
		const lastDays = movements.value
			.filter((m: Movements): boolean => {
				const today = new Date();
				const oldDate = today.setDate(today.getDate() - 30);

				return m.time > oldDate;
			})
			.map((m: Movements): number => m.amount);

		return lastDays.map((m: Movements, i: number): number => {
			const lastMovements = lastDays.slice(0, i + 1);

			return lastMovements.reduce(
				(suma: number, movement: number): number => suma + movement,
				0
			);
		});
	});
	const totalAmount = computed((): number =>
		movements.value.reduce(
			(suma: number, m: Movements): number => suma + m.amount,
			0
		)
	);

	const create = (movement: Movements): void => {
		movements.value.push(movement);
		save();
	};
	const remove = (id: number): void => {
		const index = movements.value.findIndex(
			(m: Movements): boolean => m.id === id
		);
		movements.value.splice(index, 1);
		save();
	};
	const save = (): void => {
		localStorage.setItem("movements", JSON.stringify(movements.value));
	};
	const select = (el: number): void => {
		amount.value = el;
	};

	onMounted((): void => {
		const movementsMounted = JSON.parse(localStorage.getItem("movements"));

		if (Array.isArray(movementsMounted)) {
			movements.value = movementsMounted.map((m: Movements): Movements => {
				return { ...m, time: new Date(m.time) };
			});
		}
	});
</script>

<style lang="scss" scoped></style>
