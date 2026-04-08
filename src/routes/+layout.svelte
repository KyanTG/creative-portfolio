<script>
	import '$lib/global.css';
	import Header from '$lib/components/header.svelte';
	let { children } = $props();
</script>

<main>
	<Header />
</main>

{@render children()}
