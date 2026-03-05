<script>
    import projects from '$lib/data/projects.json';
</script>

<section class="project-articles">
    {#each projects as project}
        <div class="project-article">
        <!-- change to picture with changed images to webp etc -->
            <img class="project-image" src={project.image} alt={project.title} />
        </div>
    {/each}
</section>

