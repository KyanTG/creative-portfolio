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
        width: 10rem;
        height: 10rem;
    }

    header {
    position: fixed;
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
    padding: 0 17.5px;
}

.menu-open header {
    width: 10rem;
    height: 10rem;
}

header nav ul {
    display: flex;
    flex-direction: column;
    gap: 1rem;
    visibility: hidden;
    padding: 0;
    margin: 0;
    align-items: center;
    justify-content: center;
    height: 100%;
}
nav.nav-open ul {
    visibility: visible;
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
