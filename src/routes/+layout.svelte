<script lang="ts">
	import Header from '../components/header/header.svelte';
	import '../app.css';
</script>

<Header>
	<slot />
</Header>

<style>
    :global(img) {
        max-height: 500px;
        max-width: 500px;
    }
</style>