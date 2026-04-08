<script>
    import projects from '$lib/data/projects.json';
</script>

<main onmousemove={(e) => { e.currentTarget.style.setProperty('--x', `${e.clientX}px`); e.currentTarget.style.setProperty('--y', `${e.clientY}px`);}}>
    <section class="project-articles">
        {#each projects as project}
            <div class="project-article">
                <div class="animation-wrapper">
                    <a href={project.website} target="_blank">
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
        width: 100%;
    }

    .project-articles {
        display: grid;
        grid-template-columns: repeat(2, 1fr);
        row-gap: 20vw;
        place-items: center;
        padding-top: 20rem;

        @media ( min-width: 700px ) {
            grid-template-columns: repeat(6, 1fr);
            grid-template-rows: repeat(4, auto);
            row-gap: 10vw;
        }

        @media ( min-width: 1024px ) {
            grid-template-columns: repeat(8, 1fr);
        }
    }

    .project-article {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
        width: fit-content;
        height: fit-content;
        cursor: pointer;
    }

    .animation-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        border-radius: 100%;
        border: 2vw solid var(--primary-color);
        outline: 1vw solid var(--secondary-color);
        animation: dropper linear both;
        animation-timeline: view();
        animation-range: entry 10% entry 80%;
    }

    @keyframes dropper {
        0% { 
            transform: translateY(600px); 
        }

        80% {
            transform: translateY(400);
        }

        100% { 
            transform: translateY(0); 
        }
    }

    /* Touch devices — name always visible, centered inside the circle */
    .content {
        pointer-events: none;
        background: var(--primary-color);
        border-radius: 1rem;
        border: solid 0.25rem var(--secondary-color);
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        opacity: 1;
        z-index: 10;
        padding: 0.5rem 1rem;
        width: auto;
    }

    h3 {
        opacity: 1;
        white-space: nowrap;
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
        }

        .project-article:hover .content {
            opacity: 1;
            width: 100%;
            max-width: fit-content;
        }

        h3 {
            opacity: 0;
            transition-delay: 0.2s;
        }

        .project-article:hover .content h3 {
            opacity: 1;
        }
    }

    .project-article:nth-of-type(1) {
        grid-column: 1 / -1;

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
        width: 60vw;
        height: 60vw;
        object-fit: cover;
        object-position: top;
        border-radius: 50%;

        @media ( min-width: 700px ) {
            width: 40vw;
            height: 40vw;
        }

        @media ( min-width: 1024px ) {
            width: 30vw;
            height: 30vw;
        }
    }

</style>
