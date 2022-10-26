<template>
	<div>
		<svg viewbox="0.0 300 200">
			<line stroke="#c4c4c4" stroke-width="2" x1="0" y1="75" x2="300" y2="75" />
			<polyline
				fill="none"
				stroke="#0689b0"
				stroke-width="2"
				points="0,0 100,75 200,75 300,150"
			/>
			<line
				stroke="#04b500"
				stroke-width="2"
				x1="200"
				y1="0"
				x2="200"
				y2="150"
			/>
		</svg>
		<p>Últimos 30 días</p>
	</div>
</template>

<script setup lang="ts"></script>

<style scoped lang="scss">
	svg {
		width: 100%;
	}
	p {
		text-align: center;
	}
</style>
