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
    padding-top: 6rem;
}

.home-typer-h1 {
    width: 0;
    animation: typing-home-h1-mobile 1s steps(15) forwards;

    @media (min-width: 400px) {
        animation: typing-home-h1 1s steps(15) forwards;
    }
}

.home-typer-h2 {
    width: 0;
    animation: typing-home-h2-mobile 3s steps(37) forwards;
    animation-delay: 1s;

    @media ( min-width: 400px ) {
        animation: typing-home-h2 3s steps(37) forwards;
        animation-delay: 1s;
    }
}

@keyframes typing-home-h1 {
    from { width: 0; }
    to { width: 89.5%; }
}

@keyframes typing-home-h1-mobile {
    from { width: 0; }
    to { width: 96%; }
}

@keyframes typing-home-h2 {
    from { width: 0;  }
    to { width: 76%; }
}

@keyframes typing-home-h2-mobile {
    from { width: 0; }
    to { width: 100%; }
}

</style>