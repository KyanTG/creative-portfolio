<script>
	import '$lib/global.css';
	import Header from '$lib/components/header.svelte';
	let { children } = $props();
</script>

<main>
	<Header />
</main>

{@render children()}

<style>
	:global(main) {
		padding-inline: 1rem;
		width: 100%;

		@media ( min-width: 700px ) {
			padding-inline: 2rem;
		}

		@media ( min-width: 1024px ) {
			padding-inline: 3rem;
		}
	}
</style>
