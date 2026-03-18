<script>
    import personal from '$lib/data/personal-header.json';
    let h1Done = false;
    let h2Done = false;
</script>


<section class="personal-header">
    <h1 class="home-typer-h1 h1-typer-style" class:done={h1Done} on:animationend={() => h1Done = true}>
        {personal.name}
    </h1>
    <h2 class="home-typer-h2 h2-typer-style" class:done={h2Done} on:animationend={() => h2Done = true}>
        {personal.role}
    </h2>
</section>


<style>

.personal-header {
    padding-top: 11rem;
}

.home-typer-h1 {
    animation: typing-home-mobile-h1 1s steps(15) forwards;

    @media (min-width: 458px) {
        animation: typing-home 1s steps(15) forwards;
    }
}

.home-typer-h2 {
    animation: typing-home-mobile-h2 3s steps(37) forwards;
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
    from { width: 0; visibility: visible; }
    to { width: 76%; visibility: visible; }
}

@keyframes typing-home-two-mobile {
    from { width: 0; visibility: visible; }
    to { width: 100%; visibility: visible; }
}

</style>