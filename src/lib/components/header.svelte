<script>
    import { onMount } from 'svelte';

    onMount(() => {
        const openB = document.querySelector(".menu");

        openB.onclick = () => {
            const deN = document.querySelector("nav");
            deN.classList.toggle("nav-open");
            document.body.classList.toggle('menu-open');
        };
    });
</script>

<header>
    <!-- hamburger menu -->
    <button class="menu" tabindex="0" aria-label="Menu"> 
        <span></span>
        <span></span>
        <span></span>
        <span></span>
    </button>

    <nav>
        <ul>
          <li>
            <a href="/">Home</a>
          </li>
          <li>
            <a href="/portfolio">Portfolio</a>
          </li>
          <li>
          </li>
        </ul>
      </nav>
</header>

<style>
    header {
        position: fixed;
        height: 4.5rem;
        width: 4.5rem;
        background:var(--primary-color);
        z-index: 10; 
        right: 20px;
        top: 20px;
        padding-inline: 20px;
        padding-block: 20px;
        border: 3px solid var(--primary-color);
        border-radius: 4rem;
    }

    :global(.menu-open) header {
        width: 10rem;
        height: 10rem;
    }

    nav {
        display: none;
    }

    nav.nav-open {
        display: block; 
    }

    .menu {
        display: grid;
        grid-template-rows: repeat(4, 1fr);
        grid-template-columns: repeat(4, 1fr);
        position: absolute;
        background: var(--secondary-color);
        height: 4.5rem;
        width: 4.5rem;
        right: 20px;
        row-gap: 5px;
        column-gap: 5px;
        z-index: 10;
        border: none;
        border-radius: 50%;
    }

    .menu:hover {
        cursor: pointer;
    }

    .menu span {
        display: block;
        background: var(--primary-color);
        height: 1rem;
        width: 1rem;
        border-radius: 100%;
        cursor: pointer;
    }

    .menu span:nth-of-type(1)  {
        grid-column: 2/3;
        grid-row: 2/3;
    }

    .menu span:nth-of-type(2)  {
        grid-column: 3/4;
        grid-row: 2/3;
    }

    .menu span:nth-of-type(3)  {
        grid-column: 2/3;
        grid-row: 3/4;
    }

    .menu span:nth-of-type(4)  {
        grid-column: 3/4;
        grid-row: 3/4;
    }
</style>
