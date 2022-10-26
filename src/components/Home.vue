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
					<Graphic />
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
	import { ref } from "vue";

	const amount = ref(10000);
	const totalAmount = ref(20000);
	const movements = ref([
		{
			id: 1,
			title: "Movimiento 1",
			description: "Deposito de salario",
			amount: 1000,
		},
		{
			id: 2,
			title: "Movimiento 2",
			description: "Deposito de honorarios",
			amount: 500,
		},
		{
			id: 3,
			title: "Movimiento 3",
			description: "Comida",
			amount: -100,
		},
		{
			id: 4,
			title: "Movimiento 4",
			description: "Colegiatura",
			amount: -1000,
		},
		{
			id: 5,
			title: "Movimiento 5",
			description: "Reparación equipo",
			amount: -1000,
		},
	]);
</script>

<style lang="scss" scoped></style>
