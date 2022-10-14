<template>
	<h4>{{ text }}</h4>
</template>

<script lang="ts" setup>
	import { defineProps, toRefs } from "vue";

	const props = defineProps({
		text: {
			type: String,
			required: true,
		},
	});

	toRefs(props);
</script>

<style scoped lang="scss"></style>
