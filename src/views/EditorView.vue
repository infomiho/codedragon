<script setup>
import Editor from '@/components/Editor.vue';
import { useRoute } from 'vue-router';
const route = useRoute();
const id = route.params.id;
</script>

<template>
	<div class="layout">
		<header>Editing {{ id }}</header>
		<Editor :id="id" />
	</div>
</template>

<style scoped>
.layout {
	width: 100vw;
	height: 100vh;
	display: grid;
	grid-template-rows: auto 1fr;
}

.layout header {
	padding: 1rem;
}
</style>
