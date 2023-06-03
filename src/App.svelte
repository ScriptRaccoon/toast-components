<script lang="ts">
	import Header from "./lib/components/Header.svelte";
	import Menu from "./lib/components/Menu.svelte";
	import Toast from "./lib/components/Toast.svelte";
</script>

<Toast position="top-right" />

<Header />

<main>
	<Menu />
</main>

<style>
	main {
		max-width: 32rem;
		margin-inline: auto;
	}
</style>
