<script>
    import { page } from '$app/stores';
    import projects from '$lib/data/projects.json';

    let project = projects.find(p => p.slug === $page.params.slug);
</script>

<main>
    {#if project}
        <article class="project-container">
            <h1>{project.title}</h1>
            <p class="description">{project.description}</p>

            <section>
                <img class="website-phone" src={project.websitePhone} alt={project.title}>
                <img class="website-tablet" src={project.websiteTablet} alt={project.title}>
                <img class="website-desktop" src={project.websiteDesktop} alt={project.title}>
            </section>

            <a href={project.website} target="_blank" class="visit-link">Visit Live Project</a>
            <a href="/projects" class="back-link">Back to Projects</a>
        </article>
    {:else}
        <article>
            <h1>Project Not Found</h1>
            <a href="/projects">Back to Projects</a>
        </article>
    {/if}
</main>

<style>
    main {
        padding-inline: 2rem;
    }

    h1 {
        padding-top: 6rem;
    }

    article {
        display: flex;
        flex-direction: column;
    }

    p {
        font-size: 16px;
        color: var(--secondary-color);
    }
</style>
