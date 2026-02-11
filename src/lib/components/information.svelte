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

            articles.forEach((article, i) => {
                if (i === 0) return; 

                const yDirection = (i % 2 !== 0) ? 200 : -200;
                const target = article.querySelector(".shape-mask");

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
        <div class="shape-mask">
            <div class="content-stabilizer">
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

    .shape-mask {
        position: relative;
        width: clamp(17em, 25vw, 45em); 
        height: clamp(17em, 25vw, 45em); 
        overflow: hidden; 
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        animation: cornerShapes 5s infinite linear;
    }

    .content-stabilizer {
        width: 100%;
        height: 100%;
        animation: counterRotate 5s infinite linear;
    }

    .article-style {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
        padding: 3rem; 
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

    @keyframes cornerShapes {
      0% {
        border-radius: 20em;
        corner-shape: squircle;
        rotate: 0deg;
      }
      25% {
        border-radius: 100%;
        corner-shape: round;
      }
      50% {
        border-radius: 20em;
        corner-shape: squircle;
      }
      75% {
        border-radius: 100%;
        corner-shape: round;
      }
      100% {
        border-radius: 20em;
        corner-shape: squircle;
        rotate: 360deg;
      }
    }

    @keyframes counterRotate {
      0% { rotate: 0deg; }
      100% { rotate: -360deg; }
    }
</style>