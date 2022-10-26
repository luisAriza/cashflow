<template>
	<div class="modal">
		<div class="head">
			<p>Nuevo movimiento</p>
			<XMarkIcon class="icon" @click="close" />
		</div>
		<div class="body">
			<slot></slot>
		</div>
	</div>
</template>

<script setup lang="ts">
	import { XMarkIcon } from "@heroicons/vue/24/solid";
	import { defineEmits } from "vue";

	const emit = defineEmits(["close"]);
	const close = (): void => emit("close");
</script>

<style scoped lang="scss">
	.modal {
		z-index: 2;
		position: absolute;
		left: 0;
		right: 0;
		top: 0;
		bottom: 0;
		background-color: white;
	}
	.head {
		display: flex;
		justify-content: space-between;
		align-items: center;
		width: 100%;
		padding: 24px 24px;
		box-sizing: border-box;
	}
	p {
		margin: 0;
		font-size: 1.5rem;
		color: var(--brand-blue);
	}
	.icon {
		width: 24px;
		height: 24px;
	}
</style>
