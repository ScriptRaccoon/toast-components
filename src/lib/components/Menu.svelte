<script lang="ts">
	import { send_toast } from "./Toast.svelte";

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
</menu>

<style>
	menu {
		margin-top: 2rem;
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 0.5rem;
	}

	button {
		background-color: steelblue;
		color: white;
		padding: 0.5rem 1rem;
		border-radius: 0.25rem;
	}
</style>
