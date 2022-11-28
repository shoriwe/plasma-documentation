<script lang="ts">
	// --
	import { Viewer, type BytemdPlugin } from 'bytemd';
	import gfm from '@bytemd/plugin-gfm';
	import frontmatter from '@bytemd/plugin-frontmatter';
	import gemoji from '@bytemd/plugin-gemoji';
	import highlight from '@bytemd/plugin-highlight';
	import math from '@bytemd/plugin-math';
	import mediumZoom from '@bytemd/plugin-medium-zoom';
	import mermaid from '@bytemd/plugin-mermaid';
	import { TextPlaceholder } from 'flowbite-svelte';
	import { onMount } from 'svelte';
	// --

	// CSS
	import 'bytemd/dist/index.css';
	import 'github-markdown-css';
	import 'highlight.js/styles/vs.css';
	import 'katex/dist/katex.css';
	// -- Exports
	export let url: string;

	// Variables
	const plugins: BytemdPlugin[] = [
		frontmatter(),
		gemoji(),
		gfm(),
		highlight(),
		math({
			katexOptions: { output: 'html' }
		}),
		mediumZoom(),
		mermaid()
	];

	let contents: string;
	onMount(async () => {
		fetch(url)
			.then((response) => response.text())
			.then((md) => (contents = md));
	});
</script>

<div class="w-full h-full p-5">
	{#if contents}
		<template>
			<Viewer value={contents} {plugins} />
		</template>
	{:else}
		<TextPlaceholder />
	{/if}
</div>
