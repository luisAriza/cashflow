<template>
	<Layout>
		<template #header>
			<Header />
		</template>
		<template #resume>
			<Resume
				total-label="Ahorro total"
				label="label"
				:total-amount="totalAmount"
				:amount="amount"
			>
				<template #graphic>
					<Graphic :amounts="amounts" />
				</template>
				<template #action>
					<Action />
				</template>
			</Resume>
		</template>
		<template #movements>
			<Movements :movements="movements" />
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
	import { ref, computed } from "vue";

	type Movements = {
		id: number;
		title: string;
		description: string;
		amount: number;
		time: number;
	};

	const amount = ref(10000);
	const totalAmount = ref(20000);
	const movements: any = ref([
		{
			id: 1,
			title: "Movimiento 1",
			description: "Deposito de salario",
			amount: 1000,
			time: new Date("10-01-2022"),
		},
		{
			id: 2,
			title: "Movimiento 2",
			description: "Deposito de honorarios",
			amount: 500,
			time: new Date("10-01-2022"),
		},
		{
			id: 3,
			title: "Movimiento 3",
			description: "Comida",
			amount: -100,
			time: new Date("10-01-2022"),
		},
		{
			id: 4,
			title: "Movimiento 4",
			description: "Colegiatura",
			amount: -1000,
			time: new Date("10-01-2022"),
		},
		{
			id: 5,
			title: "Movimiento 5",
			description: "Reparación equipo",
			amount: -1000,
			time: new Date("10-01-2022"),
		},
		{
			id: 5,
			title: "Movimiento 6",
			description: "Comisiones",
			amount: 600,
			time: new Date("10-01-2022"),
		},
		{
			id: 5,
			title: "Movimiento 7",
			description: "Pago de un amigo",
			amount: 200,
			time: new Date("10-01-2022"),
		},
		{
			id: 5,
			title: "Movimiento 8",
			description: "Reparación equipo",
			amount: -1400,
			time: new Date("09-10-2022"),
		},
		{
			id: 5,
			title: "Movimiento 9",
			description: "Limpieza de la casa",
			amount: -50,
			time: new Date("09-11-2022"),
		},
	]);
	const amounts = computed(() => {
		const lastDays = movements.value
			.filter((m: Movements): boolean => {
				const today = new Date();
				const oldDate = today.setDate(today.getDate() - 30);

				return m.time > oldDate;
			})
			.map((m: Movements): number => m.amount);

		return lastDays.map((m: Movements, i: number): number => {
			const lastMovements = lastDays.slice(0, i);

			return lastMovements.reduce(
				(suma: number, movement: number): number => suma + movement,
				0
			);
		});
	});
</script>

<style lang="scss" scoped></style>
