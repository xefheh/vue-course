<script setup>
	const { number, word, translation, state, status } = defineProps({
		number: String,
		word: String,
		translation: String,
		state: String,
		status: String
	})

	const emit = defineEmits(['rotate', 'changeStatus']);
</script>

<template>
	<div class="card" @click="emit('rotate')">
		<div class="innerCard">
			<p class="number">{{ number }}</p>
			<p class="word">{{ word }}</p>
			<p class="rotate">Перевернуть</p>
		</div>
	</div>
</template>

<style scoped>
.card {
	color: var(--color-card-font);
	background: var(--color-card-bg);
	width: 250px;
	height: 376px;
	border-radius: 16px;

	display: grid;
	place-items: center;

	box-shadow: 0px 0px 16px 0px #0000001A;
}

.card:hover {
	box-shadow: 10px 10px 10px 0px #0000000D;
}

.innerCard {
	width: 212px;
	height: 320px;
	border: 1px solid var(--color-primary-light);
	border-radius: 12px;

	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.rotate {
	text-transform: uppercase;
	font-size: 12px;
	letter-spacing: 12%;
	font-weight: 700;

	position: absolute;

	transform: translateY(160px);
	background-color: var(--color-card-bg);
}

.number {
	font-size: 14px;
	position: absolute;
	transform: translate(-75px, -160px);
	background-color: var(--color-card-bg);
}

.word {
	font-size: 18px;
}
</style>