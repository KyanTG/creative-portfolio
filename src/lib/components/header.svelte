<script>
    let isOpen = false;

    function toggleMenu() {
        isOpen = !isOpen;
        document.body.classList.toggle('menu-open'); 
    }
</script>

<header class:menu-open={isOpen}>
    <button class="menu" on:click={toggleMenu} tabindex="0" aria-label="Menu"> 
        <span></span>
        <span></span>
        <span></span>
        <span></span>
    </button>

    <nav class:nav-open={isOpen}>
        <ul>
            <li>
                <a href="/">Home</a>
            </li>
            <li>
                <a href="/portfolio">Portfolio</a>
            </li>
            <li>
                <a href="/contact">Contact</a>
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
        right: 20px;
        top: 20px;
        border: none;
        border-radius: 50px;
        transition: all 0.3s ease 0.3s;
    }

    header.menu-open {
        width: 9.5rem;
        height: 9.5rem;
        transition-delay: 0s; 
    }

    .menu {
        display: flex;
        flex-wrap: wrap;
        align-content: center;
        gap: 5px;
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
        padding: 0 17.5px;
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
        display: grid;
        grid-template-columns: 4.5rem 4.5rem; 
        grid-template-rows: 4.5rem 4.5rem;
        gap: 0.5rem;
        width: 9.5rem;
        height: 9.5rem;
        margin: 0;
        padding: 0;
        pointer-events: none; 
    }

    nav.nav-open ul {
        pointer-events: auto;
    }

    header li {
        list-style: none;
        background: var(--secondary-color, #eee);
        height: 4.5rem;
        width: 4.5rem;
        border-radius: 50%;
        transition: all 0.3s ease-out;
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
        grid-column: 1 / 2;
        grid-row: 1 / 2;
        transform: translate(5rem, 0) scale(0);
    }

    header nav ul li:nth-of-type(2) {
        grid-column: 1 / 2;
        grid-row: 2 / 3;
        transform: translate(5rem, -5rem) scale(0);
    }

    header nav ul li:nth-of-type(3) {
        grid-column: 2 / 3;
        grid-row: 2 / 3;
        transform: translate(0, -2rem) scale(0);
    }

    header nav ul li {
        opacity: 0;
    }

    header nav ul li:nth-of-type(1) {
        grid-column: 1 / 2;
        grid-row: 1 / 2;
        transform: translate(5rem, 0) scale(0.5);
    }

    header nav ul li:nth-of-type(2) {
        grid-column: 1 / 2;
        grid-row: 2 / 3;
        transform: translate(5rem, -5rem) scale(0.5);
    }

    header nav ul li:nth-of-type(3) {
        grid-column: 2 / 3;
        grid-row: 2 / 3;
        transform: translate(0, -5rem) scale(0.5);
    }

    header nav.nav-open ul li {
        opacity: 1;
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