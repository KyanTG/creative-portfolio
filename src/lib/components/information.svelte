<script>
    import { onMount } from "svelte";
    import information from '$lib/data/personal.json';
    import gsap from 'gsap'; 
    import { ScrollTrigger } from 'gsap/ScrollTrigger';

    let scrollContainer;
    let triggerWrap; 

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);

        const mm = gsap.matchMedia();

        mm.add(
            {
                isDesktop: "(min-width: 1024px)",
                isMobile: "(max-width: 1023px)"
            },
            (context) => {
                const { isDesktop } = context.conditions;
                const xPercentMultiplier = isDesktop ? -100 : -125;

                const articles = gsap.utils.toArray(".article-wrapper", scrollContainer);

                const scroller = gsap.to(articles, {
                    xPercent: xPercentMultiplier * (articles.length - 1),
                    ease: "none",
                });

                const mainScroll = ScrollTrigger.create({
                    trigger: triggerWrap,
                    start: "top top",
                    end: () => "+=" + scrollContainer.scrollWidth,
                    pin: true,
                    animation: scroller,
                    scrub: 1,
                    invalidateOnRefresh: true
                });

                articles.forEach((article, i) => {
                    const yDirection = (i % 2 !== 0) ? 200 : -200;
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

                const onFocusIn = (e) => {
                    const wrapper = e.target.closest('.article-wrapper');
                    if (!wrapper) return;

                    const index = articles.indexOf(wrapper);
                    if (index === -1) return;

                    const progress = index / (articles.length - 1);
                    const scrollTarget = mainScroll.start + (mainScroll.end - mainScroll.start) * progress;

                    mainScroll.scroll(scrollTarget);
                };

                scrollContainer.addEventListener('focusin', onFocusIn);

                return () => {
                    scrollContainer.removeEventListener('focusin', onFocusIn);
                };
            }
        );

        return () => mm.revert();
    });
</script>

<div class="scroll-wrap" bind:this={triggerWrap}>
    <section class="horizontal-scroll-sec" bind:this={scrollContainer}>
    {#each information as info, i}
      <div class="article-wrapper">
        
        {#if i === 0}
            <div class="shape-mask anim-target">
                <div class="content-stabilizer">
                    <article class="article-style" tabindex="0">
                        {#if info.image}
                            <img src={info.image} alt="Profile" id="foto-kyan">
                        {/if}
                    </article>
                </div>
            </div>

        {:else}
            <div class="content-group anim-target">
                <div class="animated-shape"></div>
                
                <article class="article-style" tabindex="0">
                    {#if info.image}
                        <img src={info.image} alt="Project">
                    {/if}
                    {#if info.text}
                        <p class="article-tekst">{@html info.text}</p>
                    {/if}
                    {#if info.link}
                        <a id="article-portfolio-link" href={info.link} data-sveltekit-reload>Bekijk mijn projecten</a>
                    {/if}
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
        width: 100vw;
        margin-left: calc(50% - 50vw);
        height: 100vh;
    }

    .horizontal-scroll-sec { 
        display: flex; 
        width: max-content; 
        height: 100%; 
    }

    .article-wrapper { 
        display: flex; 
        align-items: center; 
        justify-content: center; 
        width: 100vw; 
        height: 100vh; 
        margin-right: 25vw; /* Mobile-first: gap between items */
    }

    .article-wrapper:last-child {
        margin-right: 0;
    }

    @media (min-width: 1024px) {
        .article-wrapper {
            margin-right: 0; /* No extra space on desktop */
        }
    }

    .article-style {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 100%;
        height: 100%;
        padding: 2rem;
    }

    img {
        width: min(70vw, 70vh);
        height: min(70vw, 70vh);
        object-fit: contain;
        margin-top: 2rem;
    }

    #foto-kyan {
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: top;
        margin-top: 3rem;
    }

    p {
        font-size: clamp(0.9rem, 0.7rem + 1vw, 1.1rem);
        max-width: 85%;
        text-align: center;
        margin-top: 1rem;

        @media ( min-width: 1440px ) {
            font-size: 1.25rem;
        }
    }

    #article-portfolio-link {
        margin-top: 1rem;
        padding: 0.5rem 1.25rem;
        font-family: var(--primary-font);
        font-weight: 700;
        font-size: 0.8rem;
        color: var(--primary-color);
        background-color: var(--secondary-color);
        border-radius: 50px;
        text-decoration: none;
        transition: transform 0.2s ease, box-shadow 0.2s ease;
        box-shadow: 0 4px 15px color-mix(in srgb, var(--secondary-color) 40%, transparent);
    }

    #article-portfolio-link:hover {
        transform: scale(1.05);
        box-shadow: 0 6px 20px color-mix(in srgb, var(--secondary-color) 60%, transparent);
    }

    .shape-mask {
        position: relative;
        width: min(70vw, 70vh);
        height: min(70vw, 70vh);
        overflow: hidden;
        isolation: isolate;
        border: 1.5vw solid var(--secondary-color);
        border-radius: 50%;

        @media (min-width: 700px) {
            width: min(55vw, 70vh);
            height: min(55vw, 70vh);
            border: 0.9vw solid var(--secondary-color);
        }

        @media (min-width: 1024px) {
            width: min(40vw, 70vh);
            height: min(40vw, 70vh);
        }
    }

    .shape-mask .article-style {
        padding: 0;
    }

    .content-stabilizer {
        width: 100%;
        height: 100%;
        display: flex;
        align-items: center;
        justify-content: center;
        background: var(--primary-color);
    }

    .content-group {
        position: relative;
        width: min(70vw, 70vh);
        height: min(70vw, 70vh);
        display: flex;
        align-items: center;
        justify-content: center;

        @media (min-width: 700px) {
            width: min(55vw, 70vh);
            height: min(55vw, 70vh);
        }

        @media (min-width: 1024px) {
            width: min(40vw, 70vh);
            height: min(40vw, 70vh);
        }
    }

    .animated-shape {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        border: 1.5vw solid var(--secondary-color);
        border-radius: 50%;

        @media (min-width: 700px) {
            border: 0.9vw solid var(--secondary-color);
        }
        pointer-events: none;
        z-index: 0;
    }

    .content-group .article-style {
        z-index: 1;
        position: relative;
    }

    @supports (corner-shape: squircle) {
        .shape-mask,
        .animated-shape {
            animation: cornerShapes 5s infinite linear;
        }

        .content-stabilizer {
            animation: counterRotate 5s infinite linear;
        }
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