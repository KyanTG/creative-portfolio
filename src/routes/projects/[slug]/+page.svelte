<script>
    import { page } from '$app/state';
    import projects from '$lib/data/projects.json';

    let project = $derived(projects.find(p => p.slug === page.params.slug));
</script>

<main>
    {#if project}
        <article class="project-container">
            <h1>{project.title}</h1>
                <article class="description-card">
                    <p class="description">{project.description}</p>
                    {#if project.stack}
                        <ul class="stack-list">
                            {#each project.stack as tech}
                                <li class="stack-item">{tech}</li>
                            {/each}
                        </ul>
                    {/if}
                </article>

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

            <section class="buttons">
                {#if project.website}
                    <a href={project.website} target="_blank" rel="noopener noreferrer" class="visit-link">Visit Live Project</a>
                {/if}
                <a href="/projects" class="back-link" data-sveltekit-reload>Back to Projects</a>
            </section>
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
        padding-bottom: 0;
    }

    h1 {
        max-width: 250px;

        @media ( min-width: 400px ) {
            max-width: fit-content;
        }
    }

    .description-card {
        position: relative;
        max-width: 700px;
        margin-top: 2rem;
        padding: 1.5rem;
        border: 2px solid var(--secondary-color);
        border-radius: 12px;
    }

    .description {
        margin: 0;
    }

    .stack-list {
        position: absolute;
        left: 0.75rem;
        bottom: 0;
        transform: translateY(50%);
        display: flex;
        justify-content: flex-start;
        gap: 0.35rem;
        list-style: none;
        padding: 0;
        margin: 0;

        @media ( min-width: 400px ) {
            left: 1.5rem;
            gap: 0.5rem;
        }

        @media ( min-width: 700px ) {
            gap: 0.75rem;
        }
    }

    .stack-item {
        padding: 0.15rem 0.5rem;
        border-radius: 50px;
        font-family: var(--primary-font);
        background: var(--secondary-color);
        color: var(--primary-color);
        font-weight: bold;
        font-size: 0.6rem;

        @media ( min-width: 400px ) {
            padding: 0.2rem 0.6rem;
            font-size: 0.65rem;
        }

        @media ( min-width: 700px ) {
            padding: 0.25rem 0.7rem;
            font-size: 0.7rem;
        }
    }

    .buttons {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        height: 100vh;
    }

    .visit-link {
        padding: 1rem 2.5rem;
        font-family: var(--primary-font);
        font-weight: 700;
        font-size: 1rem;
        color: var(--primary-color);
        background-color: var(--secondary-color);
        border-radius: 50px;
        text-decoration: none;
        transition: transform 0.2s ease, box-shadow 0.2s ease;
        box-shadow: 0 4px 15px color-mix(in srgb, var(--secondary-color) 40%, transparent);
    }

    .visit-link:hover {
        transform: scale(1.05);
        box-shadow: 0 6px 20px color-mix(in srgb, var(--secondary-color) 60%, transparent);
    }

    .back-link {
        margin-top: 1.5rem;
        font-family: var(--primary-font);
        font-size: 0.9rem;
        color: var(--secondary-color);
        text-decoration: none;
        opacity: 0.7;
        transition: opacity 0.2s ease;
    }

    .back-link:hover {
        opacity: 1;
    }

    .phone-ring-track,
    .desktop-ring-track {
        margin-top: 20rem;
    }

    .phone-ring,
    .desktop-ring {
        display: grid;
        gap: 1.5rem;
        padding-inline: 1rem;
    }

    .phone-ring {
        grid-template-columns: repeat(2, 1fr);
        max-width: 500px;
        margin-inline: auto;
    }

    .desktop-ring {
        grid-template-columns: 1fr;
        max-width: 700px;
        margin-inline: auto;

        @media (min-width: 768px) {
            grid-template-columns: repeat(2, 1fr);
            max-width: 900px;
        }
    }

    .phone-ring-item,
    .desktop-ring-item {
        width: 100%;
        border-radius: 20px;
        border: 3px solid var(--primary-color);
        outline: 3px solid var(--secondary-color);
        object-fit: contain;
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
            --radius: 135px;
            width: 130px;
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
                --radius: 280px;
                width: 200px;
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
