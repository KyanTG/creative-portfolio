<script>
    import Hometyper from '$lib/components/homepage-typer.svelte';
    import Information from '$lib/components/information.svelte';
    import Footer from '$lib/components/footer.svelte';
</script>

<main>
    <Hometyper/>

    <Information/>

    <Footer/>
</main>

<style>

main {
    padding-inline: 2rem;
    width: 100%;

    @media ( min-width: 700px ) {
        padding-inline: 3rem;
    }

    @media ( min-width: 1024px ) {
        padding-inline: 4rem;
    }
}

</style>