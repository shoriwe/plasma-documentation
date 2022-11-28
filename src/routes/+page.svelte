<script lang="ts">
    import Viewer from "../components/markdown/viewer.svelte";

    const readme: string = "https://raw.githubusercontent.com/shoriwe/plasma/main/README.md";
</script>


<Viewer url={readme}/>
