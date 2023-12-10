<script>
	import { marked } from 'marked';
	import { onMount } from 'svelte';

	import { basicSetup, EditorView } from 'codemirror';
	import { markdown } from '@codemirror/lang-markdown';
	import { languages } from '@codemirror/language-data';
	import { indentWithTab } from '@codemirror/commands';
	import { keymap } from '@codemirror/view';

	let htmlPreview;
	let markdownInput = '# Marked in the browser\n\nRendered by **marked**.';

	onMount(() => {
		htmlPreview = marked.parse(markdownInput);

		// The Markdown parser will dynamically load parsers
		// for code blocks, using @codemirror/language-data to
		// look up the appropriate dynamic import.
		let view = new EditorView({
			doc: "Hello\n\n```javascript\nlet x = 'y'\n```",
			extensions: [basicSetup, keymap.of([indentWithTab]), markdown({ codeLanguages: languages })],
			parent: document.body
		});
	});

	function handleTextInput(event) {
		markdownInput = event.currentTarget.value;
		htmlPreview = marked.parse(markdownInput);
	}
</script>

<svelte:head>
	<title>Mmmmm</title>
</svelte:head>

<main>
	<div>
		<h2 class="header">Input</h2>
		<textarea cols="80" rows="15" on:input={handleTextInput}>{markdownInput}</textarea>
	</div>
	<div>
		<h2 class="header">Preview</h2>
		{@html htmlPreview}
	</div>

	<h2 class="header">CodeMirror</h2>
<!-- CodeMirror editor automatically goes here. Gotta figure out how to make it more explicit	-->
</main>

<style>
	h2.header {
		color: red;
	}
</style>
