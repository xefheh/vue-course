<script setup>
const { size = 24 } = defineProps(['size']);
</script>

<template>
	<svg :style="{ scale: size / 24 }" width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
<path fill-rule="evenodd" clip-rule="evenodd" d="M15.461 14.389L14.4 15.45L11.999 13.051L9.599 15.447L8.539 14.386L10.938 11.991L8.539 9.593L9.6 8.532L12 10.931L14.401 8.534L15.461 9.596L13.061 11.991L15.461 14.389ZM12 2.25C6.624 2.25 2.25 6.624 2.25 12C2.25 17.376 6.624 21.75 12 21.75C17.376 21.75 21.75 17.376 21.75 12C21.75 6.624 17.376 2.25 12 2.25Z" fill="#D00303"/>
</svg>


</template>