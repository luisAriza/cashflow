<template>
	<div class="header">
		<slot name="header"></slot>
	</div>
	<div class="resume">
		<slot name="resume"></slot>
	</div>
	<div
		class="movements"
		:class="showMovements ? 'show-movements' : 'hidden-movements'"
	>
		<div class="head" @click="showMovements = !showMovements">
			<div class="grip"></div>
		</div>
		<div class="body" v-show="showMovements">
			<slot name="movements"></slot>
		</div>
	</div>
</template>

<script lang="ts" setup>
	import { ref } from "vue";

	const showMovements = ref(false);
</script>

<style lang="scss" scoped>
	.header,
	.resume,
	.movements {
		display: flex;
		justify-content: space-around;
		align-items: center;
		padding: 14px 0;
		box-sizing: border-box;
	}
	.header {
		position: fixed;
		width: 100vw;
	}
	.resume {
		min-height: 100vh;
	}
	.movements {
		z-index: 1;
		position: absolute;
		flex-direction: column;
		bottom: 0;
		width: 100vw;
		background-color: white;
		box-shadow: 0 -8px 16px #e5e5e5;
		border-radius: 24px;
	}
	.show-movements {
		animation: show 0.6s;
	}
	@keyframes show {
		from {
			transform: translateY(75vh);
		}
		to {
			transform: translateY(0);
		}
	}
	.hidden-movements {
		animation: hidden 0.4s;
	}
	@keyframes hidden {
		from {
			transform: translateY(-75vh);
		}
		to {
			transform: translateY(0);
		}
	}
	.movements .head {
		display: flex;
		justify-content: center;
		align-items: center;
		padding: 24px;
		width: 100%;
		box-sizing: border-box;
	}
	.movements .body {
		height: 75vh;
		width: 100%;
		background: black;
	}

	.movements .head .grip {
		width: 120px;
		height: 8px;
		background-color: #e5e5e5;
		border-radius: 4px;
	}
</style>
