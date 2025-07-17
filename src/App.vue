<script setup>
import { onMounted, ref } from "vue";
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"

const API_URL = 'http://localhost:8080/api/random-words'

const cards = ref([]);

const score = ref(100);

onMounted(async () => {
	const result = await fetch(API_URL);
	const resultData = await result.json()

	let id = 1;

	cards.value = resultData.map(data => ({
		number: id++,
		word: data.word,
		translation: data.translation,
		status: "pending",
		state: "closed"
	}));
})

</script>

<template>
	<header class="header">
		<h1 class="name">Запомни слово</h1>
		<Score :score="score"/>
	</header>
	<main class="main">
		<div class="cards">
			<Card v-for="card in cards" v-bind="card" :key="card.number"/>
		</div>
		<Button
			bg-color="#008bfe"
			bg-hover-color="#006fcb"
			text-color="#ffffff">
			Начать игру
		</Button>
	</main>
</template>

<style scoped>
.header {
	display: flex;
	padding: 8px 16px;
	align-items: center;
}

.name {
	text-transform: uppercase;
	color: var(--color-font-header);
	font-size: 16px;
	font-weight: 700;
	margin-left: 0;
	margin-right: auto;
}

.cards {
	display: grid;
	grid-template-columns: 1fr 1fr 1fr 1fr;
	gap: 10px;
}

.main {
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
	flex-shrink: 0;
}
</style>
