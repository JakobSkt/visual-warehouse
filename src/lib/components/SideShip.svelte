<script lang="ts">
    import { slide } from "svelte/transition";
    import { shortcuts } from "svelte-keyboard-shortcuts";

    let { open = $bindable(false), oppositePanelOpen = $bindable() } = $props();

</script>

<button use:shortcuts={{ keys: ['s'] }} class="absolute h-[80vh] w-[5vw] items-center justify-center rounded-l-default translate-y-38 translate-x-5 top-0 right-0 bg-ship-500 dark:bg-ship-700 p-2 cursor-pointer hover:translate-x-0 transition-all z-50" onclick={() => { open = true; oppositePanelOpen = false }}>
    <h4 class="font-title text-h4 text-grey-100 rotate-90 -translate-y-4"> SHIP </h4>
</button>

{#if open}
    <div transition:slide={{ axis: 'x' }} class="absolute h-[80vh] w-[50vw] items-center justify-center rounded-l-default translate-y-38 top-0 right-0 bg-ship-500 dark:bg-ship-700 p-2 transition-all z-50">
        <button use:shortcuts={{ keys: ['c'] }} class="bg-ship-700 dark:bg-ship-500 p-1 flex items-center justify-center rounded-large cursor-pointer float-left group hover:bg-grey-300 transition-all" onclick={() => open = false } aria-label="Minimize receive panel">
            <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-chevron-right-icon lucide-chevron-right stroke-grey-300 translate-x-0.5 group-hover:stroke-ship-700 transition-all"><path d="m9 18 6-6-6-6"/></svg>
        </button>
    </div>
{/if}

