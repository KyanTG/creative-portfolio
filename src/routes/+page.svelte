<script>
    import Hometyper from '$lib/components/homepage-typer.svelte';
    import Information from '$lib/components/information.svelte';
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
    <Hometyper/>

    <Information/>
</main>

<style>

main {
    padding-inline: 1rem;
    background: var(--primary-color);
}

</style>