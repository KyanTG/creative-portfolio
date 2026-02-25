<script>
    import Hometyper from '$lib/components/homepage-typer.svelte';
    import Information from '$lib/components/information.svelte';
    import Header from '$lib/components/header.svelte';
</script>

<main>
    <Header/>

    <Hometyper/>

    <Information/>
</main>

<style>

main {
    padding-inline: 1rem;
    /* background: var(--primary-color); */
}

</style>