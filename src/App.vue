<script setup>
import { ref } from "vue";
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"

const cards = ref([{
	number: "01",
	word: "Word",
	translation: "Слово",
	status: "pending",
	state: "closed"
}, {
	number: "02",
	word: "Word",
	translation: "Слово",
	status: "fail",
	state: "open"
}, {
	number: "03",
	word: "Word",
	translation: "Слово",
	status: "success",
	state: "open"
}, {
	number: "04",
	word: "Word",
	translation: "Слово",
	status: "pending",
	state: "open"
}]);

const score = ref(100);

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
	display: flex;
	gap: 20px;
}
</style>
