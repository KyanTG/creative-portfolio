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

            <section class="project-images">
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
    .project-container {
        display: flex;
        flex-direction: column;
    }

    h1 {
        max-width: 250px;
        padding-top: 2.5rem;

        @media ( min-width: 400px ) {
            max-width: fit-content;
        }
    }

    p {
        padding-top: 2rem;
        max-width: 700px;
    }

    .project-images {
        display: flex;
        flex-direction: column;
        padding-top: 8rem;
        width: 100%;
        row-gap: 20rem;
        padding-bottom: 20rem;
    }

    img {
        animation-timeline: view();
        object-fit: contain;
        position: sticky;
        top: 60vh;
        width: auto;
        /* height: clamp(150px, calc(150px + (100vw - 320px) / 3), 220px); */
        height: 50vw;
    }

    p {
        color: var(--secondary-color);
    }

    /* make stacking cards animation for mobile */

    /* make animation for the projects on tablet and desktop, also design that */

</style>
