<script>
    import Hometyper from '$lib/components/homepage-typer.svelte';
</script>

<svelte:head> 
    <style>

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            overflow-x: hidden;
        }

        .about {
            margin-top: 2.25em;
            margin-bottom: 2.5em;
        
            @media ( min-width: 56.25em ) {
                grid-column: 1/2;
                align-self: self-end;
                margin: 0;
            }
        }
        
    </style>
</svelte:head>


<Hometyper/>


<style>



</style>