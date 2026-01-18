<script>
    import information from '$lib/data/information.json'
</script>

<section>
    <div>
        {#each information as information}
            <div>
                <article>
                    <h3>{information.content}</h3>
                </article>
            </div>
        {/each}
    </div>
</section>