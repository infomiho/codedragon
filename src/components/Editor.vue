<script setup>
import { ref, onMounted } from 'vue';

import * as Y from 'yjs';
import { WebrtcProvider } from 'y-webrtc';
import { MonacoBinding } from 'y-monaco';

import * as monaco from 'monaco-editor';

const props = defineProps({
	id: {
		type: String,
		required: true,
	},
});

const editorElement = ref(null);
onMounted(() => {
	const ydoc = new Y.Doc();

	// Users using the same ID will share the same document
	const provider = new WebrtcProvider(props.id, ydoc);
	const ycontent = ydoc.getText('monaco');

	const editor = monaco.editor.create(editorElement.value, {
		value: '',
		language: 'typescript',
		theme: 'vs-dark',
		fontSize: 16,
		fontFamily:
			'ui-monospace, Menlo, Monaco, "Cascadia Code", "Cascadia Mono", "Segoe UI Mono", "Roboto Mono", "Oxygen Mono", "Ubuntu Monospace", "Source Code Pro","Fira Mono", "Droid Sans Mono", "Courier New", monospace',
		minimap: {
			enabled: false,
		},
		scrollBeyondLastLine: false,
	});

	// Bind Yjs to the editor model
	new MonacoBinding(ycontent, editor.getModel(), new Set([editor]), provider.awareness);
});
</script>

<template>
	<div class="editor" ref="editorElement"></div>
</template>

<style>
.editor {
	width: 100%;
	height: 100%;
}
</style>
