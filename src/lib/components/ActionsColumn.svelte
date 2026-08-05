<script lang="ts">
    import ActionItem from "$lib/components/ActionItem.svelte";
    import { slide } from "svelte/transition";

    let { open = false } = $props();

    const actions = [
        { name: "Rack", description: "Use a rack to organize your warehouse both horizontally and vertically. Can directly store pallets.", img_url: "/assets/Shelves.svg" },
        { name: "Pallet", description: "Use a pallet to store your items on racks", img_url: "/assets/Pallet.svg" },
        { name: "Blue crates", description: "Use a pallet to store your items on racks", img_url: "/assets/BlueCrate.svg" },
        { name: "Plastic wrap", description: "Use plastic wrap to protect items on pallets or blue crates.", img_url: "/assets/PlasticWrap.svg" },
    ]
</script>

<div class="absolute bottom-2 right-2 flex flex-col items-center justify-evenly w-[60px] {open ? 'h-[320px]' : 'h-[60px]'} cursor-pointer bg-grey-900 rounded-large place-self-end transition-height z-50">
    {#if open}
        {#each actions as action}
            <ActionItem {...action} />
        {/each}
    {/if}
        <button onclick={() => open = !open} aria-label="Add new item" class="cursor-pointer">
            <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-plus-icon lucide-plus stroke-grey-300 transition {open? 'rotate-45' : ''}">
                <path d="M5 12h14"/><path d="M12 5v14"/>
            </svg>
        </button>


</div>
