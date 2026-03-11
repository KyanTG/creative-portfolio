<script>
    import projects from '$lib/data/projects.json';
</script>

<main 
    onmousemove={(e) => {
        e.currentTarget.style.setProperty('--x', `${e.clientX}px`);
        e.currentTarget.style.setProperty('--y', `${e.clientY}px`);
    }}
>
    <section class="project-articles">
        {#each projects as project}
            <div class="project-article">
                <a href={project.link} target="_blank">
                    <img class="project-image" src={project.image} alt={project.title} />
                </a>
                <div class="content">
                    <h3>{project.title}</h3>
                </div>
            </div>
        {/each}
    </section>
</main>

<style>
    main {
        padding-inline: 1rem;
        --x: 0px;
        --y: 0px;
    }

    .project-articles {
        display: grid;
        grid-template-columns: repeat(8, 1fr);
        grid-template-rows: repeat(4, 1fr);
        height: 400vh;
        place-items: center;
        overflow: hidden;
    }

    .project-article {
        position: relative;
        display: flex;
        align-items: center;
        justify-content: center;
        width: fit-content;
        height: fit-content;
        border-radius: 100%;
        border: 2vw solid var(--primary-color);
        outline: 1vw solid var(--secondary-color);
        cursor: pointer;
    }

    .content {
        overflow: hidden;
        background: var(--primary-color);
        border-radius: 1rem;
        border: solid 0.25rem var(--secondary-color);
        position: fixed;
        left: var(--x);
        top: var(--y);
        opacity: 0;
        z-index: 10;
        padding: 0.5rem 1rem;
        transform: translate(1rem, -40%);
        transition: width 0.3s ease-in-out;
        transition-delay: 0.02s;
        width: 0;
    }

    .project-article:hover .content {
        opacity: 1;
        width: 25rem;
    }

    h3 {
        opacity: 0;
        white-space: nowrap;
        transition-delay: 0.2s;
        transition: opacity 0.4s ease-in-out;
    }

    .project-article:hover .content h3 {
        opacity: 1;
    }

    .project-article:nth-of-type(1) {
        grid-column: 1 / 5;
        grid-row: 1 / 2;
    }

    .project-article:nth-of-type(2) {
        grid-column: 5 / 9;
        grid-row: 2 / 3;
    }

    .project-article:nth-of-type(3) {
        grid-column: 3 / 6;
        grid-row: 3 / 4;
    }

    .project-article:nth-of-type(4) {
        grid-column: 4 / 7;
        grid-row: 4 / 5;
    }

    .project-image {
        width: 40vw;
        height: 40vw;
        object-fit: cover;
        border-radius: 50%;
    }
</style>
