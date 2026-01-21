<script>
    import information from '$lib/data/information.json'
</script>

<section>
    <div>
        {#each information as information}
            <div class="article-wrapper">
                <article>
                    <!-- <img src="{information.image}" alt="picture of kyan gijtenbeek"> -->
                    <h3>{information.content}</h3>
                </article>
            </div>
        {/each}
    </div>
</section>

<style>

    section {
        overflow: hidden; 
        background: var(--main-color-normal);
        margin-block: 34vh;
    }

    div:nth-of-type(1) {
        display: flex;
        flex-direction: row;
        width: 500vw; 
        height: 100vh;
    }



    .article-wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100vw;
        height: 100vh;
    }
    
    article {

        display: flex;
        align-items: center;
        justify-content: center;
        flex-direction: column;
        width: 17.188em;
        height: 17.188em;
        padding: 0.5em;
        border-radius: 100%;
        border: 5px solid var(--secondary-color);

        /* make container queries */

        /* @media ( min-width: 700px ) {
            width: 25em;
            height: 25em;
            border: 10px solid var(--secondary-color);
        }

        @media ( min-width: 1000px ) {
            width: 30em;
            height: 30em;
            border: 12.5px solid var(--secondary-color);
        }

        @media ( min-width: 1300px ) {
            height: 35em;
            width: 35em;
            border: 15px solid var(--secondary-color);
        } */
    }

    h3 {
        color: var(--secondary-color);
    }

</style>