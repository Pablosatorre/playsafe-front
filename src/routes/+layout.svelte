<script lang="ts">
	import '../app.css';
	import { Toaster } from '$lib/components/ui/sonner/index.js';
	import favicon from '$lib/assets/favicon.png';
	import { ModeWatcher } from 'mode-watcher';

	let { children } = $props();
</script>

<svelte:head>
	<link rel="icon" href={favicon} />
</svelte:head>

<Toaster theme="dark" richColors />
<ModeWatcher defaultMode={'dark'} />

{@render children()}
