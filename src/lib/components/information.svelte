<script>
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger"; 
    import { onMount } from "svelte";
    import information from '$lib/data/information.json';
    gsap.registerPlugin(ScrollTrigger);

    

    onMount(() => {
        const horizontal = document.querySelector(".horizontal-scroll-sec");

        function scrollAmount() {
            let horizontalScrollWidth = horizontal.scrollWidth;
            return -(horizontalScrollWidth - window.innerWidth)
        }

        const scroller = gsap.to(horizontal, {
            x: scrollAmount,
            duration: 3,
            ease: "none"
        });

        ScrollTrigger.create({
            trigger: ".scroll-wrap",
            start: "top",
            end: () => `+=${scrollAmount() * -1}`,
            pin: true,
            animation: scroller,
            scrub: 1,
            invalidateOnRefresh: true
        });

        gsap.from(".article-wrapper-two", {
            y: 200,
            opacity: 0,
            duration: 1,
            ease: "power2.out",
            scrollTrigger: {
            trigger: ".article-wrapper-two",
            containerAnimation: scroller,
            start: "left center",
            end: "center center",
            scrub: true,
        }});

        gsap.from(".article-wrapper-three", {
            y: -200,
            opacity: 0,
            duration: 1,
            ease: "power2.out",
            scrollTrigger: {
            trigger: ".article-wrapper-three",
            containerAnimation: scroller,
            start: "left center",
            end: "center center",
            scrub: true,
        }});

        gsap.from(".article-wrapper-four", {
            y: 300,
            opacity: 0,
            duration: 1,
            ease: "rough",
            scrollTrigger: {
            trigger: ".article-wrapper-four",
            containerAnimation: scroller,
            start: "left center",
            end: "center center",
            scrub: true,
        }});

        gsap.from(".article-wrapper-five", {
            y: -300,
            opacity: 0,
            duration: 1,
            ease: "power2.out",
            scrollTrigger: {
            trigger: ".article-wrapper-five",
            containerAnimation: scroller,
            start: "left center",
            end: "center center",
            scrub: true,
        }});
    })

</script>

<div class="scroll-wrap">
    <section class="horizontal-scroll-sec">
    
    {#each information as info, i}
      <div class="article-wrapper article-wrapper-{i + 1}">
        <article class="article-style article-style-{i + 1}">

            {#if info.image}
                <img src={info.image} alt="Profile" id="foto-kyan">
            {/if}

            {#if info.header}
                <h3 class="header-article">{info.header}</h3>
            {/if}

            {#if info.text}
                <p class="article-tekst">{@html info.text}</p>
            {/if}

            {#if info.link}
                <a id="article-portfolio-link" href={info.link}>Bekijk mijn portfolio!</a>
            {/if}

        </article>
      </div>
    {/each}

    </section>
</div>

<style>

    section {
        overflow: hidden;
        background: var(--primary-color);
        margin-block: 34vh;
    }

    .article-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100vw;
        height: 100vh;
    }

    .article-style-1 {
        position: relative;
        background: var(--secondary-color);
    }

    img {   
        width: clamp(17em, 25vw, 35em); 
        height: clamp(17em, 25vw, 35em); 
        border-radius: 100%;
        object-fit: contain;
    }

    .header-article {
        display: flex;
        justify-content: center;
        align-items: center;
        position: absolute;
        color: var(--primary-color);
        background: var(--secondary-color);
        width: 10em;
        height: 10em;
        border-radius: 4em;
        corner-shape: scoop;
    }
    

    .article-style {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        width: clamp(17em, 25vw, 35em); 
        height: clamp(17em, 25vw, 35em); 
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        border-radius: 100%;
    }

    p {
        color: var(--secondary-color);
        font-size: clamp(1rem, 0.8rem + 1vw, 1.2rem); 
        max-width: clamp(170px, 100px + 10vw, 247px);
        margin-left: 0;
        margin-top: 1rem;
}

</style>