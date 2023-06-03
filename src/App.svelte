<script lang="ts">
	import Header from "./lib/components/Header.svelte";
	import Menu from "./lib/components/Menu.svelte";
	import Toast, {
		type toast_position,
	} from "./lib/components/Toast.svelte";

	let position: toast_position = "top-right";
</script>

<Toast {position} />
<Header />

<main>
	<Menu bind:position />
</main>

<style>
	main {
		max-width: 32rem;
		margin-inline: auto;
	}
</style>
