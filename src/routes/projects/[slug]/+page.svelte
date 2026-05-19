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

            <section class="phone-ring-track" style="--count: 4;">
                <div class="phone-ring-stage">
                    <div class="phone-ring">
                        <img class="phone-ring-item" style="--i: 0;" src={project.websitePhoneOne} alt={project.title}>
                        <img class="phone-ring-item" style="--i: 1;" src={project.websitePhoneTwo} alt={project.title}>
                        <img class="phone-ring-item" style="--i: 2;" src={project.websitePhoneThree} alt={project.title}>
                        <img class="phone-ring-item" style="--i: 3;" src={project.websitePhoneFour} alt={project.title}>
                    </div>
                </div>
            </section>

            <!-- Desktop pictures whole website macbook 14 inch -->

            <section class="project-images-desktop">
                <img class="styling-showcase website-desktop" src={project.websiteDesktopOne} alt={project.title}>
                <img class="styling-showcase website-desktop" src={project.websiteDesktopTwo} alt={project.title}>
                <img class="styling-showcase website-desktop" src={project.websiteDesktopThree} alt={project.title}>
                <img class="styling-showcase website-desktop" src={project.websiteDesktopFour} alt={project.title}>
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

    .project-images-desktop {
        display: flex;
        flex-direction: column;
        padding-top: 8rem;
        width: 100%;
        row-gap: 20rem;
        padding-bottom: 20rem;
    }

    @supports (view-timeline: --phone-ring) {

    .phone-ring-track {
        position: relative;
        height: 400vh;
        margin-top: 10rem;
        view-timeline-name: --phone-ring;
    }

    .phone-ring-stage {
        position: sticky;
        top: 0;
        height: 100vh;
        display: grid;
        place-items: center;
        perspective: 1400px;
        overflow: hidden;
    }

    .phone-ring {
        --radius: 150px;
        position: relative;
        width: 150px;
        aspect-ratio: 9 / 19;
        transform-style: preserve-3d;
        animation: phone-ring-spin linear both;
        animation-timeline: --phone-ring;
        animation-range: entry 100% exit 100%;
    }

    @media (min-width: 768px) {
        .phone-ring {
            --radius: 360px;
            width: 260px;
        }
    }

    @keyframes phone-ring-spin {
        from { transform: rotateY(0deg); }
        to { transform: rotateY(-360deg); }
    }

    .phone-ring-item {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        object-fit: contain;
        border-radius: 20px;
        backface-visibility: hidden;
        transform: rotateY(calc(var(--i) * (360deg / var(--count)))) translateZ(var(--radius));
    }
}

    .website-desktop {
        object-fit: contain;
        width: fit-content;
        height: 50vw;
    }

    .styling-showcase {
        /* border-radius: 1.5rem;
        box-shadow: 0 0 3rem var(--secondary-color); */
        animation-timeline: view();
    }

    p {
        color: var(--secondary-color);
    }

    /* make stacking cards animation for mobile */

    /* make animation for the projects on tablet and desktop, also design that */

</style>
