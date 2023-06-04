<script lang="ts" context="module">
	import { writable } from "svelte/store";

	export type toast_variant = "info" | "success" | "error";
	export type toast_position =
		| "top-left"
		| "top-center"
		| "top-right"
		| "bottom-left"
		| "bottom-center"
		| "bottom-right";

	export type toast = {
		id: string;
		title: string;
		description: string;
		variant: toast_variant;
		duration: number;
	};

	export const default_toast = {
		title: "",
		description: "",
		variant: "info",
		duration: 3000,
	} as const;

	let toast_items = writable<toast[]>([]);

	export function send_toast(toast: Partial<toast>): void {
		const id = Math.random().toString(36).slice(2);
		const _toast: toast = {
			...default_toast,
			...toast,
			id,
		};

		toast_items.update((items) => [...items, _toast]);

		setTimeout(() => {
			delete_toast(_toast);
		}, _toast.duration);
	}

	function delete_toast(toast: toast) {
		toast_items.update((items) =>
			items.filter((t) => t.id != toast.id)
		);
	}
</script>

<script lang="ts">
	export let position: toast_position = "top-left";

	import { fly } from "svelte/transition";

	$: offset_y = position.includes("top") ? -50 : 50;
</script>

<div
	class="container {position.replace('-', ' ')}"
	aria-live="assertive"
>
	{#each $toast_items as toast (toast.id)}
		<button
			class="toast {toast.variant}"
			transition:fly={{ y: offset_y, duration: 200 }}
			on:click={() => delete_toast(toast)}
		>
			{#if toast.title}
				<h2 class="title">{toast.title}</h2>
			{/if}
			<p>{toast.description}</p>
		</button>
	{/each}
</div>

<style>
	button {
		border: none;
		background: none;
		font-family: inherit;
		font-size: inherit;
		cursor: pointer;
	}

	.container {
		position: fixed;
		z-index: 10000;
		pointer-events: none;
		padding: 1rem;
		display: flex;
		gap: 1rem;
	}

	.container.top {
		top: 0;
		flex-direction: column;
	}

	.container.bottom {
		bottom: 0;
		flex-direction: column-reverse;
	}

	.container.left {
		left: 0;
		align-items: start;
	}

	.container.center {
		left: 0;
		right: 0;
		align-items: center;
	}

	.container.right {
		right: 0;
		align-items: end;
	}

	.toast {
		text-align: left;
		display: block;
		width: fit-content;
		max-width: 20rem;
		border-radius: 0.25rem;
		box-shadow: 0.1rem 0.1rem 0.4rem #0003;
		padding: 0.5rem 1rem;
		pointer-events: initial;
	}

	.toast.info {
		background-color: #fff;
		color: #000;
	}

	.toast.success {
		background-color: rgb(46, 165, 46);
		color: white;
	}

	.toast.error {
		background-color: rgb(223, 58, 58);
		color: white;
	}

	.title {
		font-size: inherit;
		margin-bottom: 0.5rem;
	}
</style>
