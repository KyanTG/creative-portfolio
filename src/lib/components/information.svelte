<script>
    import { gsap } from "gsap";
    import { ScrollTrigger } from "gsap/ScrollTrigger"; 
    import { onMount } from "svelte";
    import information from '$lib/data/information.json';

    gsap.registerPlugin(ScrollTrigger);

    let scrollContainer;
    let triggerWrap; 

    onMount(() => {
        let ctx = gsap.context(() => {
            // 1. Horizontal Scroll Setup
            const articles = gsap.utils.toArray(".article-wrapper", scrollContainer);
            const totalScroll = -100 * (articles.length - 1);

            const scroller = gsap.to(articles, {
                xPercent: totalScroll, 
                ease: "none",
            });

            ScrollTrigger.create({
                trigger: triggerWrap,
                start: "top top",
                end: () => "+=" + scrollContainer.scrollWidth,
                pin: true,
                animation: scroller,
                scrub: 1,
                invalidateOnRefresh: true
            });

            // 2. Vertical "Fly In" Animation Setup
            articles.forEach((article, i) => {
                if (i === 0) return; 

                // Odd = 200 (Up), Even = -200 (Down)
                const yDirection = (i % 2 !== 0) ? 200 : -200;
                
                // Target the NEW group wrapper so both border and text move together
                const target = article.querySelector(".content-group");

                gsap.from(target, {
                    y: yDirection,
                    opacity: 0,
                    duration: 1,
                    ease: "power2.out",
                    scrollTrigger: {
                        trigger: article,
                        containerAnimation: scroller, 
                        start: "left center",
                        end: "center center",
                        scrub: true,
                    }
                });
            });

        }, scrollContainer);

        return () => ctx.revert(); 
    });
</script>

<div class="scroll-wrap" bind:this={triggerWrap}>
    <section class="horizontal-scroll-sec" bind:this={scrollContainer}>
    {#each information as info, i}
      <div class="article-wrapper">
        
        <div class="content-group">
            
            <div class="animated-shape"></div>
            
            <article class="article-style">
                {#if info.image}
                    <img src={info.image} alt="Profile" id="foto-kyan">
                {/if}

                {#if info.text}
                    <p class="article-tekst">{@html info.text}</p>
                {/if}

                {#if info.link}
                    <a id="article-portfolio-link" href={info.link}>Bekijk mijn portfolio!</a>
                {/if}
            </article>
        </div>

      </div>
    {/each}
    </section>
</div>

<style>
    .scroll-wrap {
        overflow: hidden;
        width: 100%;
        height: 100vh;
    }

    .horizontal-scroll-sec {
        display: flex;
        flex-wrap: nowrap;
        width: max-content; 
        height: 100%;
    }

    section {
        background: var(--primary-color);
    }

    .article-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100vw;
        height: 100vh;
        flex-shrink: 0;
    }

    /* --- NEW CSS LOGIC --- */

    /* The Group: Holds everything together for the Up/Down animation */
    .content-group {
        position: relative;
        width: clamp(17em, 25vw, 45em); 
        height: clamp(17em, 25vw, 45em); 
        display: flex;
        align-items: center;
        justify-content: center;
    }

    /* The Spinner: Absolutely positioned behind the content */
    .animated-shape {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        border-radius: 100%;
        animation: cornerShapes 5s infinite linear; /* SPINNING HAPPENS HERE */
        pointer-events: none; /* Ensures you can click links through it */
    }

    /* The Content: Sitting on top, NOT spinning */
    .article-style {
        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        width: 100%;
        height: 100%;
        z-index: 1; /* Puts text above the border */
        /* Note: No border or animation here anymore */
    }

    img {   
        width: clamp(17em, 25vw, 35em); 
        height: clamp(17em, 25vw, 35em); 
        border-radius: 100%;
        object-fit: contain;
    }

    p {
        color: var(--secondary-color);
        font-size: clamp(1rem, 0.8rem + 1vw, 1.2rem); 
        max-width: clamp(170px, 100px + 10vw, 247px);
        margin-left: 0;
        margin-top: 1rem;
    }

    @keyframes cornerShapes {
      0% { border-radius: 20em; corner-shape: squircle; rotate: 0deg; }
      25% { border-radius: 100%; corner-shape: round; }
      50% { border-radius: 20em; corner-shape: squircle; }
      75% { border-radius: 100%; corner-shape: round; }
      100% { border-radius: 20em; corner-shape: squircle; rotate: 360deg; }
    }
</style>