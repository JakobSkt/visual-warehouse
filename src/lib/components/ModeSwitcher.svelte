<script lang="ts">
    import { setMode, mode } from "mode-watcher";
    import { shortcuts } from "svelte-keyboard-shortcuts";

    function handleModeChange() {
        if (mode.current === "light") {
            setMode("dark");
        } else {
            setMode("light");
        }
    }
</script>

<button onclick={handleModeChange} use:shortcuts={{ keys: ['m'] }} class="absolute w-10 h-10 top-2 right-2 lg:top-16 lg:left-8 flex items-center justify-center p-2 rounded-full bg-brand-300 dark:bg-grey-700 cursor-pointer">
    {#if mode.current === "dark"}
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-sun-icon lucide-sun"><circle cx="12" cy="12" r="4"/><path d="M12 2v2"/><path d="M12 20v2"/><path d="m4.93 4.93 1.41 1.41"/><path d="m17.66 17.66 1.41 1.41"/><path d="M2 12h2"/><path d="M20 12h2"/><path d="m6.34 17.66-1.41 1.41"/><path d="m19.07 4.93-1.41 1.41"/></svg>
    {:else}
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-moon-icon lucide-moon"><path d="M20.985 12.486a9 9 0 1 1-9.473-9.472c.405-.022.617.46.402.803a6 6 0 0 0 8.268 8.268c.344-.215.825-.004.803.401"/></svg>
    {/if}
</button>