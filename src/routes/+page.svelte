<script>
	import { marked } from 'marked';
	import { onMount } from 'svelte';

	let markdown;

	onMount(() => {
		markdown = marked.parse('# Marked in the browser\n\nRendered by **marked**.');
	});
</script>

<svelte:head>
	<title>Mmmmm</title>
</svelte:head>

<style>
  h2.header {
    color: red;
  }
</style>

<main>
	<div>
		<h2 class="header">Input</h2>
		<textarea></textarea>
	</div>
	<div>
		<h2 class="header">Preview</h2>
		{@html markdown}
	</div>
</main>
