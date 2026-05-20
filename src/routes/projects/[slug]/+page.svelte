<script>
    import { page } from '$app/state';
    import projects from '$lib/data/projects.json';

    let project = $derived(projects.find(p => p.slug === page.params.slug));
</script>

<main>
    {#if project}
        <article class="project-container">
            <h1>{project.title}</h1>
            <p class="description">{project.description}</p>

            {#if project.websitePhoneOne}
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
            {/if}

            {#if project.websiteDesktopOne}
                <section class="desktop-ring-track" style="--count: 4;">
                    <div class="desktop-ring-stage">
                        <div class="desktop-ring">
                            <img class="desktop-ring-item" style="--i: 0;" src={project.websiteDesktopOne} alt={project.title}>
                            <img class="desktop-ring-item" style="--i: 1;" src={project.websiteDesktopTwo} alt={project.title}>
                            <img class="desktop-ring-item" style="--i: 2;" src={project.websiteDesktopThree} alt={project.title}>
                            <img class="desktop-ring-item" style="--i: 3;" src={project.websiteDesktopFour} alt={project.title}>
                        </div>
                    </div>
                </section>
            {/if}

            {#if project.website}
                <a href={project.website} target="_blank" rel="noopener noreferrer" class="visit-link">Visit Live Project</a>
            {/if}
            <a href="/projects" class="back-link" data-sveltekit-reload>Back to Projects</a>
        </article>
    {:else}
        <article>
            <h1>Project Not Found</h1>
            <a href="/projects" data-sveltekit-reload>Back to Projects</a>
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

        @media ( min-width: 400px ) {
            max-width: fit-content;
        }
    }

    .description {
        padding-top: 2rem;
        max-width: 700px;
    }

    @supports (view-timeline: --phone-ring) {

        .phone-ring-track,
        .desktop-ring-track {
            position: relative;
            height: 400vh;
            margin-top: 10rem;
        }

        .phone-ring-track { view-timeline-name: --phone-ring; }
        .desktop-ring-track { view-timeline-name: --desktop-ring; }

        .phone-ring-stage,
        .desktop-ring-stage {
            position: sticky;
            top: 0;
            height: 100vh;
            display: grid;
            place-items: center;
            perspective: 1400px;
            overflow: hidden;
        }

        .phone-ring,
        .desktop-ring {
            position: relative;
            transform-style: preserve-3d;
            animation: phone-ring-spin linear both;
            animation-range: entry 100% exit 100%;
        }

        .phone-ring {
            --radius: 150px;
            width: 150px;
            aspect-ratio: 9 / 19;
            animation-timeline: --phone-ring;
        }

        .desktop-ring {
            --radius: 180px;
            width: 240px;
            aspect-ratio: 16 / 9;
            animation-timeline: --desktop-ring;
        }

        @media (min-width: 768px) {
            .phone-ring {
                --radius: 360px;
                width: 260px;
            }

            .desktop-ring {
                --radius: 360px;
                width: 460px;
            }
        }

        @media (min-width: 1024px) {
            .desktop-ring {
                --radius: 480px;
                width: 600px;
            }
        }

        @keyframes phone-ring-spin {
            from { transform: rotateY(0deg); }
            to { transform: rotateY(-360deg); }
        }

        .phone-ring-item,
        .desktop-ring-item {
            position: absolute;
            inset: 0;
            height: 100%;
            object-fit: contain;
            border-radius: 20px;
            backface-visibility: hidden;
            transform: rotateY(calc(var(--i) * (360deg / var(--count)))) translateZ(var(--radius));
        }
    }
</style>
