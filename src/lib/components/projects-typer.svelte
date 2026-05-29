<script>
    import projectTyper from '$lib/data/projects-header.json';
    let h1Done = $state(false);
</script>

<section class="project-header">
    <h1 class="project-typer-h1 h1-typer-style" class:done={h1Done} onanimationend={() => h1Done = true}>{projectTyper.name}</h1>

</section>

<style>

    .project-typer-h1 {
        interpolate-size: allow-keywords;
        width: 0;
        animation: typing-project-h1 0.6s steps(9) 0.8s forwards;
    }

    @keyframes typing-project-h1 {
        from { width: 0; border-right-color: var(--secondary-color); }
        to { width: max-content; border-right-color: var(--secondary-color); }
    }
</style>