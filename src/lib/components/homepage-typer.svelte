<script>
    import personal from '$lib/data/personal-header.json';
    let h1Done = $state(false);
    let h2Done = $state(false);
</script>


<section class="personal-header">
    <h1 class="home-typer-h1 h1-typer-style" class:done={h1Done} onanimationend={() => h1Done = true}>
        {personal.name}
    </h1>
    <h2 class="home-typer-h2 h2-typer-style" class:done={h2Done} onanimationend={() => h2Done = true}>
        {personal.role}
    </h2>
</section>


<style>

.home-typer-h1 {
    width: 0;
    animation: typing-home-h1-mobile 1s steps(15) 0.8s forwards;

    @media (min-width: 400px) {
        animation: typing-home-h1 1s steps(15) 0.8s forwards;
    }
}

.home-typer-h2 {
    width: 0;
    animation: typing-home-h2-mobile 3s steps(37) forwards;
    animation-delay: 1.8s;

    @media ( min-width: 400px ) {
        animation: typing-home-h2 3s steps(37) forwards;
        animation-delay: 1.8s;
    }
}

@keyframes typing-home-h1 {
    from { width: 0; border-right-color: var(--secondary-color); }
    to { width: 89.5%; border-right-color: var(--secondary-color); }
}

@keyframes typing-home-h1-mobile {
    from { width: 0; border-right-color: var(--secondary-color); }
    to { width: 96%; border-right-color: var(--secondary-color); }
}

@keyframes typing-home-h2 {
    from { width: 0; border-right-color: var(--secondary-color); }
    to { width: 76%; border-right-color: var(--secondary-color); }
}

@keyframes typing-home-h2-mobile {
    from { width: 0; border-right-color: var(--secondary-color); }
    to { width: 100%; border-right-color: var(--secondary-color); }
}

</style>