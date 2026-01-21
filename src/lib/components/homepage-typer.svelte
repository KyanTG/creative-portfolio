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
    color: var(--secondary-color);
    overflow: hidden; 
    white-space: nowrap; 
    border-right: 2px solid var(--secondary-color); 
}

.h2-typer-style {
    color: var(--secondary-color);
    width: 0;
    overflow: hidden;
    white-space: nowrap;
    border-right: 0.1vw solid var(--secondary-color-light);
}

.home-typer-h1 {
    animation: typing-home-mobile 1s steps(15) forwards;

    @media (min-width: 458px ) {
        animation: typing-home 1s steps(15) forwards;
    }
}

.home-typer-h2 {
    animation: typing-home-two-mobile 3s steps(37) forwards;
    animation-delay: 1s;

    @media ( min-width: 458px ) {
        animation: typing-home-two 3s steps(37) forwards;
        animation-delay: 1s;
    }
}

@keyframes typing-home {
    from { width: 0; }
    to { width: 87.5%; }
}

@keyframes typing-home-mobile {
    from { width: 0; }
    to { width: 96%; }
}

@keyframes typing-home-two {
    from { width: 0; }
    to { width: 76%; }
}

@keyframes typing-home-two-mobile {
    from { width: 0; }
    to { width: 100%; }
}

</style>