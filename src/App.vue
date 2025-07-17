<script setup>
import { onMounted, ref } from "vue";
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"
import Error from "./components/Error.vue"

const API_URL = 'http://localhost:8080/api/random-words'

const cards = ref([]);

const error = ref(null);

const score = ref(100);

onMounted(async () => {
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

</script>

<template>
	<header class="header">
		<h1 class="name">Запомни слово</h1>
		<Score :score="score"/>
	</header>
	<main class="main">
		<Error :error></Error>
		<div class="cards">
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
