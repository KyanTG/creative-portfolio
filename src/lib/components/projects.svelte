<script>
    import projects from '$lib/data/projects.json';
</script>

<main>
    <section class="project-articles">
        {#each projects as project}
            <div class="project-article">
            <!-- change to picture with changed images to webp etc -->
                <img class="project-image" src={project.image} alt={project.title} />
                <!-- <a href={project.website} target="_blank">click</a> -->
            </div>
        {/each}
    </section>
</main>

<style>

    main {
        padding-inline: 1rem;
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
        display: flex;
        align-items: center;
        justify-content: center;
        width: fit-content;
        height: fit-content;
        border-radius: 100%;
        border: 1vw solid var(--primary-color);
        outline: 1vw solid var(--secondary-color);
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
