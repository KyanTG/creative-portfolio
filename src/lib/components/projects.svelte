<script>
    import { onMount } from 'svelte';
    import projects from '$lib/data/projects.json';

    onMount(() => {
        window.onmousemove = function(e) {
            const article = e.target.closest('.project-article');
            const allContent = document.querySelectorAll('.content');

            if (article) {
                const muis = article.querySelector('.content');
                if (muis) {
                    muis.classList.add('visible');
                    const offset = article.getBoundingClientRect();
                    const tip = 15;
                    muis.style.top = (e.clientY - offset.top + tip) + 'px';
                    muis.style.left = (e.clientX - offset.left + tip) + 'px';
                }
            } else {
                allContent.forEach(c => c.classList.remove('visible'));
            }
        }
    });
</script>

<main>
    <section class="project-articles">
        {#each projects as project}
            <div class="project-article">
            <!-- change to picture with changed images to webp etc -->
                <img class="project-image" src={project.image} alt={project.title} />
                <!-- <a href={project.website} target="_blank">click</a> -->
                <div class="content">
                    <h2>{project.title}</h2>
                </div>
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
        position: relative; /* added to ensure content positions relative to this */
        display: flex;
        align-items: center;
        justify-content: center;
        width: fit-content;
        height: fit-content;
        border-radius: 100%;
        border: 1vw solid var(--primary-color);
        outline: 1vw solid var(--secondary-color);
    }

    .content {
        position: absolute;
        pointer-events: none; /* prevents content from flickering */
        opacity: 0;
        transition: opacity 0.2s ease-in-out;
        z-index: 10;
        white-space: nowrap;
    }

    .content.visible {
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
