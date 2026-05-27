<script>
    import projectTyper from '$lib/data/projects-header.json';
    let h1Done = $state(false);
</script>

<section class="project-header">
    <h1 class="project-typer-h1 h1-typer-style" class:done={h1Done} onanimationend={() => h1Done = true}>{projectTyper.name}</h1>

</section>

<style>

    .project-typer-h1 {
        width: 0;
        animation: typing-project-mobile-h1 0.6s steps(9) 0.8s forwards;

        @media ( min-width: 400px ) {
            animation: typing-project-h1 0.6s steps(9) 0.8s forwards;
        }
    }

    @keyframes typing-project-mobile-h1 {
        from { width: 0; border-right-color: var(--secondary-color); }
        to { width: 62%; border-right-color: var(--secondary-color); }
    }

    @keyframes typing-project-h1 {
        from { width: 0; border-right-color: var(--secondary-color); }
        to { width: 55%; border-right-color: var(--secondary-color); }
    }
</style>