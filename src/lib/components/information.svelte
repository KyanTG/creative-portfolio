<script>
    import { onMount } from "svelte";
    import information from '$lib/data/personal.json';
    import gsap from 'gsap'; 
    import { ScrollTrigger } from 'gsap/ScrollTrigger';

    let scrollContainer;
    let triggerWrap; 

    onMount(() => {
        gsap.registerPlugin(ScrollTrigger);

        let ctx = gsap.context(() => {
            const articles = gsap.utils.toArray(".article-wrapper", scrollContainer);
            
            // Mobile-first: default is double space, desktop is single
            let xPercentMultiplier = -200; // Default for mobile
            if (window.matchMedia("(min-width: 1124px)").matches) {
                xPercentMultiplier = -100; // Desktop
            }

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

            scrollContainer.addEventListener('focusin', (e) => {
                const wrapper = e.target.closest('.article-wrapper');
                if (!wrapper) return;

                const index = articles.indexOf(wrapper);
                if (index === -1) return;

                if (scrollContainer.scrollLeft !== 0) scrollContainer.scrollLeft = 0;
                if (triggerWrap.scrollLeft !== 0) triggerWrap.scrollLeft = 0;

                const progress = index / (articles.length - 1);
                const scrollTarget = mainScroll.start + (mainScroll.end - mainScroll.start) * progress;

                window.scrollTo({
                    top: scrollTarget,
                    behavior: 'auto' 
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
                        <a id="article-portfolio-link" href={info.link}>Bekijk mijn projecten</a>
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
        width: 100%; 
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
        margin-right: 100vw; /* Mobile-first: double space by default */
    }

    @media (min-width: 1124px) {
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
        color: var(--secondary-color);
        font-size: clamp(0.9rem, 0.7rem + 1vw, 1.1rem);
        max-width: 85%;
        text-align: center;
        margin-top: 1rem;

        @media ( min-width: 1440px ) {
            font-size: 1.25rem;
        }
    }

    #article-portfolio-link {
        margin-top: 0.5rem;
        color: var(--secondary-color);
    }

    .shape-mask {
        position: relative;
        width: min(70vw, 70vh);
        height: min(70vw, 70vh);
        overflow: hidden;
        isolation: isolate;
        border: clamp(5px, 1vw, 15px) solid var(--secondary-color);
        animation: cornerShapes 5s infinite linear;

        @media (min-width: 1124px) {
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
        animation: counterRotate 5s infinite linear;
        background: var(--primary-color);
    }

    .content-group {
        position: relative;
        width: min(70vw, 70vh); 
        height: min(70vw, 70vh);
        display: flex;
        align-items: center;
        justify-content: center;

        @media (min-width: 1124px) {
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