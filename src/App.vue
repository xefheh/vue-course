<script setup>
import { onMounted, ref, provide, computed } from "vue";
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"
import Error from "./components/Error.vue"
import Button from "./components/Button.vue"
import { scoreSymbol } from './constants';

const API_URL = 'http://localhost:8080/api/random-words'

const cards = ref([]);

const error = ref(null);

const isStart = ref(false);

const score = ref(0);

provide(scoreSymbol, score);

const start = () => {
	cards.value = [];
	fetchWords();
	score.value = 0;
	isStart.value = true;
}

const fetchWords = async () => {
	try {
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
	} catch(err) {
		error.value = err;
	}
}

onMounted(async () => {
	fetchWords();
})

const onRotate = (number) => {
	cards.value = 
		cards.value.map(card => card.number === number ? {
			...card,
			state: "opened"
		} : card);
}

const onChangeStatus = ({number, status}) => {
	cards.value = 
		cards.value.map(card => card.number === number ? {
			...card,
			status: status
		} : card);
}

const isAllCardsNotPending = computed(() => {
	return cards.value.length > 0 && cards.value.every(card => card.status !== 'pending');
})


</script>

<template>
	<header class="header">
		<h1 class="name">Запомни слово</h1>
		<Score :score="score"/>
	</header>
	<main class="main">
		<Button 
			v-if="!isStart"
			bg-color="#008bfe"
			bg-hover-color="#006fcb"
			text-color="#ffffff"
			@click="start">Начать игру</Button>
		<Button 
			v-else-if="isAllCardsNotPending"
			bg-color="#008bfe"
			bg-hover-color="#006fcb"
			text-color="#ffffff"
			@click="start">Начать заново</Button>
		<div v-else class="cards">
			<Error :error></Error>
			<Card v-for="card in cards" v-bind="card" :key="card.number" @rotate="onRotate" @change-status="onChangeStatus"/>
		</div>
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
