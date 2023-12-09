<script>
	import { marked } from 'marked';
	import { onMount } from 'svelte';
	import './prism.js';

	let htmlPreview;
	let markdown = '# Marked in the browser\n\nRendered by **marked**.';

	onMount(() => {
		htmlPreview = marked.parse(markdown);
		Prism.highlightAll();
	});

	function handleTextInput(event) {
		markdown = event.currentTarget.value;
		htmlPreview = marked.parse(markdown);
		Prism.highlightAll();
	}
</script>

<svelte:head>
	<title>Mmmmm</title>

	<script>
		window.Prism = window.Prism || {};
		window.Prism.manual = true;
	</script>
</svelte:head>

<main>
	<div>
		<h2 class="header">Input</h2>
		<textarea cols="80" rows="15" on:input={handleTextInput}>{markdown}</textarea>
		<div>
			<h3>Hmm the highlighted version only works on first render</h3>
			<pre><code class="language-markdown">{markdown}</code></pre>
			<pre><code>{markdown}</code></pre>
		</div>
	</div>
	<div>
		<h2 class="header">Preview</h2>
		{@html htmlPreview}
	</div>
</main>

<style>
	@import './prism.css';

	h2.header {
		color: red;
	}
</style>
