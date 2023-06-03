<script lang="ts">
	import { send_toast, type toast_position } from "./Toast.svelte";

	export let position: toast_position = "top-left";

	function show_info() {
		send_toast({
			title: "Information",
			description:
				"You can use this component in any Svelte project",
		});
	}

	function show_success() {
		send_toast({
			title: "Login successful",
			description: "You can now open your dashboard",
			variant: "success",
		});
	}

	function show_error() {
		send_toast({
			title: "Internal server error",
			description: "Database connection failed",
			variant: "error",
		});
	}

	function show_short() {
		send_toast({
			description: "Well done!",
		});
	}

	function show_long() {
		send_toast({
			title: "Patience exercise",
			description: "This toast stays for 10 seconds ...",
			duration: 10000,
		});
	}
</script>

<menu>
	<button on:click={show_info}>Send info toast</button>
	<button on:click={show_success}>Send success toast</button>
	<button on:click={show_error}>Send error toast</button>
	<button on:click={show_short}>Send short toast</button>
	<button on:click={show_long}>Send long toast</button>
	<div>
		<label for="select">Position</label>
		<select id="select" bind:value={position}>
			<option value="top-left">top-left</option>
			<option value="top-center">top-center</option>
			<option value="top-right">top-right</option>
			<option value="bottom-left">bottom-left</option>
			<option value="bottom-center">bottom-center</option>
			<option value="bottom-right">bottom-right</option>
		</select>
	</div>
</menu>

<style>
	menu {
		margin-top: 2rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 1rem;
	}

	button {
		border: none;
		background: none;
		font-family: inherit;
		font-size: inherit;
		cursor: pointer;
		background-color: steelblue;
		color: white;
		padding: 0.5rem 1rem;
		border-radius: 0.25rem;
	}

	select,
	option {
		font-family: inherit;
		font-size: inherit;
	}

	select {
		padding: 0.25rem;
	}
</style>
