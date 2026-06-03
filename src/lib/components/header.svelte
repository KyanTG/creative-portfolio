<script>
    let isOpen = $state(false);

    function toggleMenu() {
        isOpen = !isOpen;
        document.body.classList.toggle('menu-open');
    }

    function closeMenu() {
        isOpen = false;
        document.body.classList.remove('menu-open');
    }
</script>

<header class:menu-open={isOpen}>
    <button class="menu" onclick={toggleMenu} tabindex="0" aria-label="Menu">
        <span></span>
        <span></span>
        <span></span>
        <span></span>
    </button>

    <nav class:nav-open={isOpen}>
        <ul>
            <li>
                <a href="/" onclick={closeMenu} data-sveltekit-reload>Home</a>
            </li>
            <li>
                <a href="/projects" onclick={closeMenu} data-sveltekit-reload>Projecten</a>
            </li>
            <li>
                <a href="/contact" onclick={closeMenu} data-sveltekit-reload>Contact</a>
            </li>
        </ul>
    </nav>
</header>


<style>

    header {
        position: fixed;
        height: 4.5rem;
        width: 4.5rem;
        z-index: 10;
        right: var(--hamburger-right);
        top: var(--hamburger-top);
        border: none;
        overflow: hidden;
        transition: all 0.3s ease 0.3s;
    }

    header.menu-open {
        width: 9.5rem;
        height: 9.5rem;
        transition-delay: 0s; 
        background: var(--primary-color);
        border-radius: 36px;
    }

    .menu {
        appearance: none;
        display: grid;
        grid-template-columns: repeat(2, 1rem);
        grid-template-rows: repeat(2, 1rem);
        gap: 5px;
        place-content: center;
        position: absolute;
        top: 0;
        right: 0;
        z-index: 10;
        background-color: var(--secondary-color, #eee);
        border: none;
        height: 4.5rem;
        width: 4.5rem;
        border-radius: 50%;
        box-sizing: border-box;
        cursor: pointer;
    }

    .menu span {
        display: block;
        background: var(--primary-color, #333);
        height: 1rem;
        width: 1rem;
        border-radius: 100%;
    }

    .menu-open span {
        position: absolute;
        width: 1.25rem;
        height: 1.25rem;
        inset: 26px 0px 0px 26px;
    }

    header nav {
        height: 100%;
        width: 100%;
    }

    header nav ul {
        position: relative;
        width: 9.5rem;
        height: 9.5rem;
        margin: 0;
        padding: 0;
        pointer-events: none;
        visibility: hidden;
    }

    .menu-open a {
        font-size: 0.9rem;
        letter-spacing: -0.04em;
    }

    nav.nav-open ul {
        pointer-events: auto;
        visibility: visible;
    }

    header li {
        position: absolute;
        list-style: none;
        background: var(--secondary-color, #eee);
        height: 4.5rem;
        width: 4.5rem;
        border-radius: 50%;
        transition: all 0.3s ease-out;
        z-index: 5;
        opacity: 0;
    }

    header a {
        display: flex;
        align-items: center;
        justify-content: center;
        color: var(--primary-color, #333);
        font-size: 16px;
        text-decoration: none;
        width: 100%;
        height: 100%;
    }

    header nav ul li:nth-of-type(1) {
        top: 0;
        left: 0;
        transform: translate(calc(4.5rem + var(--hamburger-right)), 0) scale(0.5);
    }

    header nav ul li:nth-of-type(2) {
        bottom: 0;
        left: 0;
        transform: translate(calc(4.5rem + var(--hamburger-right)), calc(-4.5rem - var(--hamburger-right))) scale(0.5);
    }

    header nav ul li:nth-of-type(3) {
        bottom: 0;
        right: 0;
        transform: translate(0, calc(-4.5rem - var(--hamburger-right))) scale(0.5);
    }

    header nav.nav-open ul li {
        opacity: 1;
        z-index: 1;
    }

    header nav.nav-open ul li:nth-of-type(1) { 
        transform: translate(0, 0) scale(1);
        transition-delay: 0.05s; 
    }
    
    header nav.nav-open ul li:nth-of-type(2) { 
        transform: translate(0, 0) scale(1);
        transition-delay: 0.1s; 
    }
    
    header nav.nav-open ul li:nth-of-type(3) { 
        transform: translate(0, 0) scale(1);
        transition-delay: 0.15s; 
    }

</style>