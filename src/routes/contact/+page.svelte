<main>
    <h1>deze pagina is onder constructie.</h1>
</main>

<style>
    main {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 100vh;
        width: 100%;
        padding-inline: 2rem;

        @media ( min-width: 700px ) {
            padding-inline: 3rem;
        }

        @media ( min-width: 1024px ) {
            padding-inline: 4rem;
        }
    }
    h1 {
        color: var(--secondary-color);
        text-align: center;
    }
</style>