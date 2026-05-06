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

            <!-- Phone pictures whole website iphone 12pro -->

            <section class="project-images-phone">
                <img class="website-phone" src={project.websitePhoneOne} alt={project.title}>
                <img class="website-phone" src={project.websitePhoneTwo} alt={project.title}>
                <img class="website-phone" src={project.websitePhoneThree} alt={project.title}>
                <img class="website-phone" src={project.websitePhoneFour} alt={project.title}>
            </section>

            <!-- Desktop pictures whole website macbook 14 inch -->

            <section class="project-images-desktop">
                <img class="website-desktop" src={project.websiteDesktopOne} alt={project.title}>
                <img class="website-desktop" src={project.websiteDesktopTwo} alt={project.title}>
                <img class="website-desktop" src={project.websiteDesktopThree} alt={project.title}>
                <img class="website-desktop" src={project.websiteDesktopFour} alt={project.title}>
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

    .project-images-phone {
        display: flex;
        flex-direction: column;
        padding-top: 8rem;
        width: 100%;
        row-gap: 20rem;
        padding-bottom: 20rem;
    }

    .project-images-desktop {
        display: flex;
        flex-direction: column;
        padding-top: 8rem;
        width: 100%;
        row-gap: 20rem;
        padding-bottom: 20rem;
    }

    .website-phone {
        animation-timeline: view();
        object-fit: contain;
        position: sticky;
        top: 60vh;
        width: auto;
        height: 50vw;
    }

    .website-desktop {
        animation-timeline: view();
        object-fit: contain;
        position: sticky;
        top: 60vh;
        width: auto;
        height: 50vw;
    }

    p {
        color: var(--secondary-color);
    }

    /* make stacking cards animation for mobile */

    /* make animation for the projects on tablet and desktop, also design that */

</style>
