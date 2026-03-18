<script>
    import projectTyper from '$lib/data/projects-header.json';
    let h1Done = false;
    let h2Done = false;
</script>

<section class="project-header">
    <h1 class="project-typer-h1 h1-typer-style" class:done={h1Done} on:animationend={() => h1Done = true}>{projectTyper.name}</h1>

</section>

<style>

    .project-header {
        padding-top: 11rem;
    }

    .project-typer-h1 {
        animation: typing-project-mobile-h1 1s steps(9) forwards;
    }

    @keyframes typing-project-mobile-h1 {
        from { width: 0; }
        to { width: 53vw; }
    }

    @keyframes typing-project-mobile-h2 {
        from { width: 0; visibility: visible; }
        to { width: 100%; visibility: visible; }
    }

</style>