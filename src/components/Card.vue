<script setup>
import { scoreSymbol } from '../constants';
import CancelIcon from './CancelIcon.vue';
import OkIcon from './OkIcon.vue';
import { inject } from 'vue';

	const { number, word, translation, state, status } = defineProps({
		number: Number,
		word: String,
		translation: String,
		state: String,
		status: String
	})

	const score = inject(scoreSymbol);

	const isClosed = () => {
		return state === 'closed';
	}

	const isPending = () => {
		return status === 'pending';
	}

	const isSuccess = () => {
		return status === "success";
	}

	const emit = defineEmits(['rotate', 'changeStatus']);

	const rotate = (number) => {
		emit('rotate', number);
	}

	const setSuccess = () => {
		score.value += 10;
		emit('changeStatus', {number: number, status: 'success'});
	}

	const setFailure = () => {
		score.value -= 4;
		emit('changeStatus', {number: number, status: 'failure'});
	}
</script>

<template>
	<div :class="{pointer: isClosed()}" class="card" @click="rotate(number)">
		<div class="innerCard">
			<p class="number">{{ number }}</p>
			<p v-if="isClosed()" class="word">{{ word }}</p>
			<p v-else class="word">{{ translation }}</p>
			<p v-if="isClosed()" class="rotate">Перевернуть</p>
			<div class="iconContainer">
				<OkIcon
					v-if="isSuccess() && !isClosed()"
					class="resultIcon"  
					size="48"></OkIcon>
				<CancelIcon  
					v-if="!isSuccess() && !isPending() && !isClosed()"
					class="resultIcon"
					size="48"></CancelIcon>
			</div>
			<div v-if="!isClosed() && isPending()" class="chooseMenu">
				<button class="iconButton" @click="setFailure">
					<CancelIcon></CancelIcon>
				</button>
				<button class="iconButton" @click="setSuccess">
					<OkIcon></OkIcon>
				</button>
			</div>
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
	cursor: default;
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

.pointer {
	cursor: pointer;
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
	text-align: center;
}

.chooseMenu {
	position: absolute;

	display: flex;
	gap: 10px;
	justify-content: center;
	align-items: center;
	padding: 0 4px;

	transform: translateY(160px);
	background-color: var(--color-card-bg);
}

.iconContainer {
	position: absolute;
	transform: translateY(-157px);
	background-color: var(--color-card-bg);
}

.iconButton {
	background: none;
	border: none;
	cursor: pointer;
}

</style>