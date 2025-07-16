<script setup>
import { ref } from 'vue'
import ScoreIcon from './ScoreIcon.vue';

const { score = 100 } = defineProps({
	score: Number
 })
</script>

<template>
<div class="score">
	{{ score }}
	<ScoreIcon/>
</div>
</template>

<style scoped>
	.score {
		color: var(--primary);
		font-weight: 700;
		padding: 12px 24px;
		background-color: var(--color-primary-light);
		border-radius: 36px;

		display: flex;
		align-items: center;
		justify-content: center;
		gap: 10px;
	}
</style>