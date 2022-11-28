<script lang="ts">
	import { Navbar, NavBrand, NavLi, NavUl, NavHamburger, Skeleton } from 'flowbite-svelte';
	// https://api.github.com/repos/shoriwe/plasma/contents/docs/embedding/embedding.md
</script>

<div class="relative px-8">
	<Navbar
		navClass="px-2 sm:px-4 py-2.5 absolute w-full z-20 top-0 left-0 border-b"
		let:hidden
		let:toggle
	>
		<NavBrand href="/">
			<img src="logo.png" class="mr-3 h-6 sm:h-9" alt="plasma" />
			<span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">Plasma</span
			>
		</NavBrand>
		<NavHamburger on:click={toggle} />
		<NavUl {hidden}>
			<NavLi href="/documentation">Documentation</NavLi>
		</NavUl>
	</Navbar>
	<div style="height:100vh;" class="overflow-scroll pb-16">
		<div class="mt-20 mb-8">
			<slot />		
		</div>
	</div>
</div>