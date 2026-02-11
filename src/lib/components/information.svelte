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
            const articles = gsap.utils.toArray(".article-wrapper", scrollContainer);
            
            // Horizontal Scroll
            const scroller = gsap.to(articles, {
                xPercent: -100 * (articles.length - 1), 
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

            // Vertical "Fly In" Animation for ALL articles
            articles.forEach((article, i) => {
                // Determine direction (Up/Down)
                const yDirection = (i % 2 !== 0) ? 200 : -200;
                
                // Select the element to animate (works for both Types A and B)
                const target = article.querySelector(".anim-target");

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
        
        {#if i === 0}
            <div class="shape-mask anim-target">
                <div class="content-stabilizer">
                    <article class="article-style">
                        {#if info.image}
                            <img src={info.image} alt="Profile" id="foto-kyan">
                        {/if}
                    </article>
                </div>
            </div>

        {:else}
            <div class="content-group anim-target">
                <div class="animated-shape"></div>
                
                <article class="article-style">
                    {#if info.image}<img src={info.image} alt="Project">{/if}
                    {#if info.text}<p class="article-tekst">{@html info.text}</p>{/if}
                    {#if info.link}<a id="article-portfolio-link" href={info.link}>Bekijk mijn portfolio!</a>{/if}
                </article>
            </div>
        {/if}

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

    .article-style {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
        padding: 2rem;
        box-sizing: border-box;
    }

    img {   
        width: clamp(17em, 25vw, 35em); 
        height: clamp(17em, 25vw, 35em); 
        object-fit: contain;
    }
    
    p {
        color: var(--secondary-color);
        font-size: clamp(1rem, 0.8rem + 1vw, 1.2rem); 
        max-width: clamp(170px, 100px + 10vw, 247px);
        margin-left: 0;
        margin-top: 1rem;
        text-align: center;
    }

    .shape-mask {
        position: relative;
        width: clamp(17em, 25vw, 45em); 
        height: clamp(17em, 25vw, 45em); 
        overflow: hidden; 
        isolation: isolate; 
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        animation: cornerShapes 5s infinite linear;
    }
    
    .content-stabilizer {
        width: 100%;
        height: 100%;
        animation: counterRotate 5s infinite linear;
        background: var(--primary-color); 
    }

    .content-group {
        position: relative;
        width: clamp(17em, 25vw, 45em); 
        height: clamp(17em, 25vw, 45em); 
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .animated-shape {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        animation: cornerShapes 5s infinite linear;
        pointer-events: none; 
        z-index: 0;
    }

    .content-group .article-style {
        z-index: 1;
        position: relative;
    }

    @keyframes cornerShapes {
      0% { border-radius: 20em; corner-shape: squircle; rotate: 0deg; }
      25% { border-radius: 100%; corner-shape: round; }
      50% { border-radius: 20em; corner-shape: squircle; }
      75% { border-radius: 100%; corner-shape: round; }
      100% { border-radius: 20em; corner-shape: squircle; rotate: 360deg; }
    }
    @keyframes counterRotate {
      0% { rotate: 0deg; }
      100% { rotate: -360deg; }
    }
</style>