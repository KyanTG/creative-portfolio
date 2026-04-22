<script>
    import ProjectsTyper from "$lib/components/projects-typer.svelte";
    import Projects from "$lib/components/projects.svelte";
    import Scroll from "$lib/components/scroll.svelte";
</script>

<main>
    <ProjectsTyper />

    <Scroll />

    <Projects />
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