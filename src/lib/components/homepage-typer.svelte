<script>
    import personal from '$lib/data/personal.json'
</script>


<section class="personal">
    <h1 class="home-typer-h1 h1-typer-style">{personal.name}</h1>
    <h2 class="home-typer-h2 h2-typer-style">{personal.role}</h2>
</section>


<style>

.personal {
    padding-top: 8rem;
}

.h1-typer-style {
    border-right: 2px solid var(--secondary-color-light); 
    overflow: hidden; 
    white-space: nowrap; 
}

.h2-typer-style {
    width: 0;
    border-right: 0.1vw solid var(--secondary-color-light);
    overflow: hidden;
    white-space: nowrap;
}
</style>