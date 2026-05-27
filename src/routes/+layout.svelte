<script>
	import '$lib/global.css';
	import Header from '$lib/components/header.svelte';
	import Footer from '$lib/components/footer.svelte';
	let { children } = $props();
</script>

<Header />

{@render children()}

<Footer />

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

	:global(h1) {
		margin-top: var(--h1-top);
	}

	:global(footer) {
		padding-bottom: 1rem;
	}
</style>
