<script lang="ts">
    import LoadedPallet from "$lib/components/LoadedPallet.svelte";

    let { open = $bindable(), shelfName, detailedPalletOpen = $bindable() } = $props();
</script>

<div class="relative lg:absolute w-full lg:w-[40vw] h-full m-0 p-0 bg-grey-700 flex flex-col overflow-hidden border-2 border-grey-900 rounded-default z-40">
    <div class="fixed flex w-[84vw] ml-[18vw] lg:w-[39.5vw] lg:ml-0.5 rounded-default bg-grey-500 h-[7vh] items-center justify-between z-50 px-4 overflow-hidden">
        <h2 class="font-title text-h2 text-grey-300"> {shelfName} </h2>
        <button class="m-0 p-0  flex flex-col cursor-pointer group" aria-label="Close detailed shelf view" onclick={() => open = false}>
            <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-x-icon lucide-x stroke-grey-300 group-hover:stroke-grey-700 transition"><path d="M18 6 6 18"/><path d="m6 6 12 12"/></svg>
        </button>
    </div>

    <img src="/assets/RACKS-SIDE-VIEW.svg" class="h-[70vh] lg:h-[75vh] lg:mt-[5vh]" alt="Rack side view">

    <LoadedPallet bind:detailedPalletView = {detailedPalletOpen} />
</div>
