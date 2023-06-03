# Toast components for Svelte

This repo contains a single-file Toast component which you can copy paste into your Svelte (or SvelteKit) project.

Demo: https://toast-components.netlify.app

The file [`src/lib/components/Toast.svelte`](https://github.com/ScriptRaccoon/toast-components/blob/main/src/lib/components/Toast.svelte) contains both the rendered Toast components as well as the function with which you can send toasts.

## Usage

Embed the Toast component to your `App.svelte`.

```svelte
<script lang="ts">
	import Toast from "./lib/components/Toast.svelte";
</script>

<Toast position="top-right" />
```

You can pass one of 6 positions as a prop: `top-left` (default), `top-center`, `top-right`, `bottom-left`, `bottom-center`, `bottom-right`.

When you want to send a toast, from wherever you like, import the `send_toast` function and execute it.

```typescript
import { send_toast } from "./Toast.svelte";

send_toast({
	title: "Information",
	description: "You can use this component in any Svelte project",
});
```

Pass the following options to this function:

-   `title: string` (default: `""`)
-   `description: string` (default: `""`)
-   `variant: "info" | "success" | "error"` (default: `info`)
-   `duration: number` (default: `3000`)

If you want to customize the Toasts, just edit the Svelte component `Toast.svelte` as you like.
