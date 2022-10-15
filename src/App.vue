<template>
	<Suspense>
		<template #default>
			<Home text="Hola Vue" />
		</template>
		<template #fallBack>
			<Splashscreen />
		</template>
	</Suspense>
</template>

<script lang="ts">
	import { defineAsyncComponent } from "vue";
	import Splashscreen from "@/components/Splashscreen.vue";

	export default {
		name: "App",
		components: {
			Splashscreen,
			Home: defineAsyncComponent(
				(): Promise<{ default: unknown }> =>
					new Promise((resolve): void => {
						setTimeout((): void => {
							return resolve(import("./components/Home.vue"));
						}, 2500);
					})
			),
		},
	};
</script>

<style lang="scss">
	html,
	body,
	#app {
		min-height: 100vh;
		margin: 0;
		font-family: Arial, Helvetica, sans-serif;
	}

	* {
		--brand-green: #04b500;
		--brand-blue: #0689b0;
	}
</style>
