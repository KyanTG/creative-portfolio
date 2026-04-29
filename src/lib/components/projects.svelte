<script>
    import projects from '$lib/data/projects.json';
</script>

<main onmousemove={(e) => { e.currentTarget.style.setProperty('--x', `${e.clientX}px`); e.currentTarget.style.setProperty('--y', `${e.clientY}px`);}}>
    <section class="project-articles">
        {#each projects as project}
            <div class="project-article">
                <div class="animation-wrapper">
                    <a href="/projects/{project.slug}">
                        <img class="project-image" src={project.websiteTablet} alt={project.title} />
                    </a>
                </div>
                <div class="content">
                    <h3>{project.title}</h3>
                </div>
            </div>
        {/each}
    </section>
</main>

<style>
    main {
        --x: 0px;
        --y: 0px;
        scroll-behavior: smooth;
    }

    .project-articles {
        display: grid;
        grid-template-columns: 1fr;
        row-gap: 20vw;
        place-items: center;
        padding-top: 20rem;

        @media ( min-width: 700px ) {
            grid-template-columns: repeat(6, 1fr);
            grid-template-rows: repeat(4, 1fr);
            row-gap: 10vw;
        }

        @media ( min-width: 1024px ) {
            grid-template-columns: repeat(8, 1fr);
        }
    }

    .project-article {
        position: relative;
        display: grid;
        place-items: center;
        width: fit-content;
        height: fit-content;
        cursor: pointer;
        view-timeline-name: --article;
    }

    .animation-wrapper {
        grid-area: 1 / 1;
        display: grid;
        place-items: center;
        border-radius: 100%;
        border: 3vw solid var(--primary-color);
        outline: 1.5vw solid var(--secondary-color);
        animation: dropper linear both, dropper linear reverse forwards;
        animation-timeline: --article;
        animation-range: entry 10% entry 80%, exit 20% exit 90%;

        @media ( min-width: 700px ) {
            border: 1.8vw solid var(--primary-color);
            outline: 0.9vw solid var(--secondary-color);
        }
    }

    .animation-wrapper > a {
        grid-area: 1 / 1;
    }

    /* Touch devices — name always visible, centered inside the circle */
    .content {
        grid-area: 1 / 1;
        pointer-events: none;
        background: var(--primary-color);
        border-radius: 1rem;
        border: solid 0.25rem var(--secondary-color);
        opacity: 1;
        z-index: 10;
        padding: 0.5rem 0.5rem;
        animation: dropper linear both, dropper linear reverse forwards;
        animation-timeline: --article;
        animation-range: entry 10% entry 80%, exit 20% exit 90%;

        @media ( min-width: 700px ) {
            padding: 0.5rem 1rem;
        }
    }

    h3 {
        opacity: 1;
        white-space: nowrap;
        font-size: 0.75rem;

        @media ( min-width: 400px ) {
            font-size: 1rem;
        }

        @media ( min-width: 700px ) {
            font-size: 1rem;
        }
    }

    /* Mouse devices — cursor-following hover behaviour */
    @media (hover: hover) and (pointer: fine) {
        .content {
            overflow: hidden;
            position: fixed;
            left: var(--x);
            top: var(--y);
            opacity: 0;
            transform: translate(1rem, -40%);
            transition: width 1s ease-in-out;
            transition-delay: 0.02s;
            width: 0;
            animation: none;
        }

        .project-article:hover .content {
            opacity: 1;
            width: 100%;
            max-width: fit-content;
        }

        h3 {
            opacity: 0;
            transition-delay: 0.2s;
            font-size: 1.5rem;
        }

        .project-article:hover .content h3 {
            opacity: 1;
        }
    }

    .project-article:nth-of-type(1) {
        grid-column: 1;

        @media ( min-width: 700px ) {
            grid-column: 1 / 4;
            grid-row: 1 / 2;
        }

        @media ( min-width: 1024px ) {
            grid-column: 1 / 5;
        }
    }

    .project-article:nth-of-type(2) {
        grid-column: 1 / -1;

        @media ( min-width: 700px ) {
            grid-column: 4 / 7;
            grid-row: 2 / 3;
        }

        @media ( min-width: 1024px ) {
            grid-column: 5 / 9;
        }
    }

    .project-article:nth-of-type(3) {
        grid-column: 1 / -1;

        @media ( min-width: 700px ) {
            grid-column: 1 / 4;
            grid-row: 3 / 4;
        }

        @media ( min-width: 1024px ) {
            grid-column: 3 / 6;
        }
    }

    .project-article:nth-of-type(4) {
        grid-column: 1 / -1;

        @media ( min-width: 700px ) {
            grid-column: 4 / 7;
            grid-row: 4 / 5;
        }

        @media ( min-width: 1024px ) {
            grid-column: 4 / 7;
        }
    }

    .project-image, a {
        display: block;
        width: 70vw;
        height: 70vw;
        max-width: 350px;
        max-height: 350px;
        object-fit: cover;
        object-position: top;
        border-radius: 50%;

        @media ( min-width: 400px ) {
            width: 60vw;
            height: 60vw;
        }

        @media ( min-width: 700px ) {
            width: 40vw;
            height: 40vw;
            max-width: none;
            max-height: none;
        }

        @media ( min-width: 1024px ) {
            width: 30vw;
            height: 30vw;
        }

    }

    @keyframes dropper {
        0% {
            transform: scale(0);
        }

        80% {
            transform: scale(0.5);
        }

        100% {
            transform: scale(1);
        }
    }

</style>
