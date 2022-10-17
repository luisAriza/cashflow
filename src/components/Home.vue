<template>
	<Layout>
		<template #header>
			<Header />
		</template>
		<template #resume>
			<Resume
				total-label="Ahorro total"
				label="label"
				:total-amount="20000"
				:amount="amount"
			>
				<template #graphic> graphic </template>
				<template #action> action </template>
			</Resume>
		</template>
		<template #movements>
			<Movements />
		</template>
	</Layout>
</template>

<script lang="ts" setup>
	import Layout from "./Layout.vue";
	import Header from "./Header.vue";
	import Resume from "./Resume/Index.vue";
	import Movements from "./Movements.vue";
	import { ref } from "vue";

	const amount = ref(10000);
</script>

<style lang="scss" scoped></style>
