<script setup>
const props = defineProps(['bgColor', 'bgHoverColor', 'textColor'])

const emit = defineEmits(['click'])
</script>

<template>
	<button 
	class="button"
	:style="{
		'--color-button-bg': props.bgColor,
		'--color-button-bg-hover': props.bgHoverColor,
		'--color-button-text': props.textColor
		}"
	@click="emit('click')">
		<slot />
	</button>
</template>

<style scoped>
	.button {
		border: none;
		border-radius: 100px;
		background: var(--color-button-bg);
		padding: 10px 16px;
		font-family: var(--font);
		font-size: 24px;
		font-weight: 400;
		color: var(--color-button-text);
		cursor: pointer;		
	}

	.button:hover {
		background: var(--color-button-bg-hover);
	}
</style>