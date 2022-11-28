<script lang="ts">
	import Viewer from '../markdown/viewer.svelte';
	import type { Documentation } from './documentation';

	export let documentation: Documentation;
</script>

{#key documentation}
	{#if documentation}
		<Viewer url={documentation.download_url} />
	{/if}
{/key}
