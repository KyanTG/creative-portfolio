<script>
    import Hometyper from '$lib/components/homepage-typer.svelte';
    import Information from '$lib/components/information.svelte';
    import Header from '$lib/components/header.svelte';
</script>

<!-- <svelte:head> 
    <style>

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            overflow-x: hidden;
        }
        
    </style>
</svelte:head> -->

<main>
    <Header/>

    <Hometyper/>

    <Information/>
</main>

<style>

main {
    padding-inline: 1rem;
    background: var(--primary-color);
}

</style>