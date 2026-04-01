<script>
    import { page } from '$app/stores';
    import projects from '$lib/data/projects.json';

    let project = projects.find(p => p.slug === $page.params.slug);
</script>

<main>
    {#if project}
        <section class="project-container">
            <h1>{project.title}</h1>
            <p class="description">{project.description}</p>
            <a href={project.website} target="_blank" class="visit-link">Visit Live Project</a>
            <a href="/projects" class="back-link">Back to Projects</a>
        </section>
    {:else}
        <section>
            <h1>Project Not Found</h1>
            <a href="/projects">Back to Projects</a>
        </section>
    {/if}
</main>

<style>
    main {
        padding-inline: 2rem;
    }

    h1 {
        padding-top: 6rem;
    }

    section {
        display: flex;
        flex-direction: column;
    }

    p {
        font-size: 16px;
        color: var(--secondary-color);
    }
</style>
