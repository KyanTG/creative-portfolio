<script>
    import Hometyper from '$lib/components/homepage-typer.svelte';
    import Information from '$lib/components/information.svelte';
</script>

<main class="home">
    <Hometyper/>

    <Information/>
</main>

<style>
    .home {
        animation: 0.8s step-end both delay-content;
    }

    @keyframes delay-content {
        from { visibility: hidden; }
        to { visibility: visible; }
    }
</style>
