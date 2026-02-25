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

    :global(.menu-open) header {
        width: 13rem;
        height: 13rem;
    }

    header {
    position: fixed;
    height: 4.5rem;
    width: 4.5rem;
    z-index: 10; 
    right: 20px;
    top: 20px;
    padding-inline: 20px;
    padding-block: 20px;
    background-color:var(--primary-color);
    border: 3px solid var(--primary-color);
    border-radius: 50px;
    /* transition: all 0.3s ease; */
    }

    .menu {
    display: flex;
    flex-wrap: wrap;
    align-content: center;
    gap: 5px;
    position: absolute;
    right: 20px;
    z-index: 10;
    background-color: var(--secondary-color);
    border: none;
    height: 4.5rem;
    width: 4.5rem;
    border-radius: 50%;
    box-sizing: border-box;
    padding: 0 17.5px;
}

header nav {
    height: 100%;
    width: 100%;
}

header nav ul {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 1fr 1fr;
    gap: 1rem;
    height: 100%;
    padding: 0;
    margin: 0;
    visibility: hidden;
}

:global(nav.nav-open) ul {
    visibility: visible;
}

header nav ul li:nth-of-type(1) {
    grid-column: 1 / 2;
    grid-row: 1 / 2;
}

header nav ul li:nth-of-type(2) {
    grid-column: 1 / 2;
    grid-row: 2 / 3;
}

header nav ul li:nth-of-type(3) {
    grid-column: 2 / 3;
    grid-row: 2 / 3;
}

header li {
    list-style: none;
    color: var(--primary-color);
    background: var(--secondary-color);
    height: 4.5rem;
    width: 4.5rem;
    border-radius: 50%;
    transition: transform 0.3s ease; 
}

header a {
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--primary-color);
    font-size: 16px;
    letter-spacing: -0.5px;
    text-decoration: none;
    width: 100%;
    height: 100%;
}

/* .menu:focus {
    outline-offset: 5px;
    outline: 2px solid var(--secondary-color-light);
} */

.menu:hover {
    cursor: pointer;
}

.menu span {
    display: block;
    background: var(--primary-color);
    height: 16px;
    width: 16px;
    border-radius: 100%;
    cursor: pointer;
}

.menu-open .menu {
    display: flex;
    align-items: center;
    justify-content: center;
}

.menu-open .menu span {
    position: absolute;
    width: 20px;
    height: 20px;
    cursor: pointer;
}
</style>
