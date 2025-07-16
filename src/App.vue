<script setup>
import { ref } from 'vue';

const date = ref(new Date())

setInterval(() => {
	date.value = new Date()
}, 1000);

</script>

<template>
{{ date }}
</template>

<style scoped>

</style>
