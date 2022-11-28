<script lang="ts">
	import { sineIn } from 'svelte/easing';
	import { Drawer, Button, CloseButton } from 'flowbite-svelte';

	import type { Documentation } from './documentation';
	import Explorer from './explorer.svelte';
	import Path from './path.svelte';
	import View from './view.svelte';

	export let baseDirectory: string;

	let location: string[] = ['/'];
	let readDir: () => void;
	let documentation: Documentation;

	// Drawer
	let hidden1: boolean = true;
	let transitionParams = {
		x: -320,
		duration: 200,
		easing: sineIn
	};
</script>

<div class="w-full h-full p-5">
	<Path bind:readDir bind:location />
	<div class="w-full p-5">
		<Explorer bind:readDir {baseDirectory} bind:location bind:documentation />
	</div>
	<View bind:documentation />
</div>
