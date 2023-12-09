<script>
	import { marked } from 'marked';
	import { onMount } from 'svelte';

  let markdown

	onMount(() => {
    markdown = marked.parse(
      '# Marked in the browser\n\nRendered by **marked**.'
    )
  })
</script>

<svelte:head>
  <title>Mmmmm</title>
</svelte:head>

<main>{@html markdown}</main>
