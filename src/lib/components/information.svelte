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

<section>
    <div>
        {#each information as info}
            <div class="article-wrapper">
                <article>
                    {#if info.image}
                        <img src={info.image} alt="picture of {info.content}">
                    {/if}
                    <h3>{info.content}</h3>
                </article>
            </div>
        {/each}
    </div>
</section>

<style>

    section {
        overflow: hidden;
        background: var(--main-color-normal);
        margin-block: 34vh;
    }
/* 
    div:nth-of-type(1) {
        display: flex;
        flex-direction: row;
        width: 500vw; 
        height: 100vh;
    } */



    .article-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100vw;
        height: 100vh;
    }
    
    /* article {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        width: 17.188em;
        height: 17.188em;
        padding: 0.5em;
        border-radius: 100%;
        border: 5px solid var(--secondary-color); 


         @media ( min-width: 700px ) {
            width: 25em;
            height: 25em;
            border: 10px solid var(--secondary-color);
        }

        @media ( min-width: 1000px ) {
            width: 30em;
            height: 30em;
            border: 12.5px solid var(--secondary-color);
        }

        @media ( min-width: 1300px ) {
            height: 35em;
            width: 35em;
            border: 15px solid var(--secondary-color);
        }
    } */

    article {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        width: clamp(17em, 25vw, 35em); 
        height: clamp(17em, 25vw, 35em); 
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        border-radius: 100%;
    }

    h3 {
        color: var(--secondary-color);
    }

    img {
        width: clamp(17em, 25vw, 35em); 
        height: clamp(17em, 25vw, 35em); 
        border-radius: 100%;
        object-fit: contain;
    }

</style>