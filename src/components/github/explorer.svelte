<script lang="ts">
	import { Li, List, ListPlaceholder } from 'flowbite-svelte';
	import { onMount } from 'svelte';
	import type { Documentation } from './documentation';

	export let baseDirectory: string;
	export let location: string[];
	export let documentation: Documentation;
	export let readDir: () => void;

	let contents: Documentation[];

	onMount(async () => {
		readDir = () => {
			const url =
				baseDirectory +
				location.slice(0, location.length - 1).join('/') +
				location[location.length - 1];
			fetch(url)
				.then((r) => r.json())
				.then((j) => (contents = j))
				.catch((error) => alert(error));
		};
	});

	function openFile(file: Documentation): () => void {
		return () => {
			documentation = file;
		};
	}

	function openDir(directory: string): () => void {
		return () => {
			location.push(directory);
			location = location;
		};
	}
</script>

{#key contents}
	{#if contents}
		<List tag="ul" class="space-y-1" list="none">
			{#each contents as file}
				<Li>
					{#if file.type === 'dir'}
						<a class="no-underline" href="" on:click={openDir(file.name)}>
							<i class="fa-solid fa-folder" />
							{file.name}
						</a>
					{:else}
						<a class="no-underline" href="" on:click={openFile(file)}>
							<i class="fa-solid fa-file" />
							{file.name}
						</a>
					{/if}
				</Li>
			{/each}
		</List>
	{:else}
		<ListPlaceholder />
	{/if}
{/key}
