<script lang="ts">
	import { Breadcrumb, BreadcrumbItem } from 'flowbite-svelte';

	export let location: string[];
	export let readDir: () => void;

	function setCurrent(index: number): () => void {
		return () => {
			location = location.slice(0, index + 1);
		};
	}

	$ : {
		location;
		if (typeof window !== undefined && readDir) {
			readDir();
		}
 	}
</script>

<Breadcrumb aria-label="Solid background breadcrumb example" solid>
	<BreadcrumbItem home
		><a class="no-underline" href="" on:click={setCurrent(0)}>Home</a></BreadcrumbItem
	>
	{#key location}
		{#each location.slice(1, location.length + 1) as dir, index}
			<BreadcrumbItem
				><a class="no-underline" href="" on:click={setCurrent(index)}>{dir}</a></BreadcrumbItem
			>
		{/each}
	{/key}
</Breadcrumb>
