<script>
    import projects from '$lib/data/projects.json';
</script>

<section class="project-articles">
    {#each projects as project}
        <article class="project-article">
            <h2>{project.title}</h2>
            <p>{project.description}</p>
        </article>
    {/each}
</section>