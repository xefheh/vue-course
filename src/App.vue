<script setup>
import { ref } from "vue";
import Button from "./components/Button.vue"
import Score from "./components/Score.vue"
import Card from "./components/Card.vue"

const cards = ref([{
	number: "01",
	word: "Word",
	translation: "Слово"
}]);

const score = ref(100);

</script>

<template>
	<header class="header">
		<h1 v-bind="cards[0]" class="name">Запомни слово</h1>
		<Score :score="score"/>
	</header>
	<main class="main">
		<Card number="01" word="word" />
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
</style>
