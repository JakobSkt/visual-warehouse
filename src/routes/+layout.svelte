<script lang="ts">
	import './layout.css';
	import favicon from '$lib/assets/favicon.svg';
    import { ModeWatcher } from 'mode-watcher';
    import { Shortcuts } from "svelte-keyboard-shortcuts";

    let { children } = $props();
</script>

<svelte:head><link rel="icon" href={favicon} /></svelte:head>
<ModeWatcher />
<Shortcuts options={{ generateKbd: false }}/>
{@render children()}
