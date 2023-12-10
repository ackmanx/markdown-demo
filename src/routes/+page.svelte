<script>
	import { marked } from 'marked';
	import { onMount } from 'svelte';

	let htmlPreview;
	let markdown = '# Marked in the browser\n\nRendered by **marked**.';

	onMount(() => {
		htmlPreview = marked.parse(markdown);
	});

	function handleTextInput(event) {
		markdown = event.currentTarget.value;
		htmlPreview = marked.parse(markdown);
	}
</script>

<svelte:head>
	<title>Mmmmm</title>
</svelte:head>

<main>
	<div>
		<h2 class="header">Input</h2>
		<textarea cols="80" rows="15" on:input={handleTextInput}>{markdown}</textarea>
	</div>
	<div>
		<h2 class="header">Preview</h2>
		{@html htmlPreview}
	</div>
</main>

<style>
	h2.header {
		color: red;
	}
</style>
