<script>
    import scrollDown from "$lib/assets/scroll-down.svg";
</script>

<section class="scroll-down">
    <a href="#">
        <img id="small-scroll" src={scrollDown} alt="scroll down">
        <img id="medium-scroll" src={scrollDown} alt="scroll down">
        <img id="big-scroll" src={scrollDown} alt="scroll down">
    </a>
</section>  

<style>

    .scroll-down {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-top: 10rem;
    }

    a {
        position: relative;
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 6rem;
        height: 10rem;
    }

    img {
        animation: moving 1.6s ease-in-out infinite;
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
</style>
