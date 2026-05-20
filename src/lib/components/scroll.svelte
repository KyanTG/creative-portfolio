<script>
    import scrollDown from "$lib/assets/scroll-down.svg";
</script>

<section class="scroll-down" aria-hidden="true">
    <div class="scroll-stack">
        <img id="small-scroll" src={scrollDown} alt="">
        <img id="medium-scroll" src={scrollDown} alt="">
        <img id="big-scroll" src={scrollDown} alt="">
    </div>
</section>

<style>

    .scroll-down {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 10rem;
    }

    .scroll-stack {
        position: relative;
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 6rem;
        height: 10rem;
        opacity: 0;
        animation: fade-in 0.4s ease forwards;
        animation-delay: 1s;
    }

    img {
        animation: moving 1.4s ease-in-out infinite;
        position: absolute;
        opacity: 0;
    }

    #small-scroll {
        animation-delay: 0.1s;
        width: 4rem;
        top: 0;
    }

    #medium-scroll {
        animation-delay: 0.2s;
        width: 5rem;
        top: 1rem;
    }

    #big-scroll {
        animation-delay: 0.3s;
        width: 6rem;
        top: 2rem;
    }

    @keyframes moving {
        0% { opacity: 0; transform: translateY(-0.4rem); }
        20% { opacity: 1; transform: translateY(0); }
        80% { opacity: 1; transform: translateY(0); }
        100% { opacity: 0; transform: translateY(0.4rem); }
    }

    @keyframes fade-in {
        from { opacity: 0; }
        to { opacity: 1; }
    }
</style>
