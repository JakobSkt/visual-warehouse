<script lang="ts">
    let { detailedShelfOpen = $bindable(), shelfName, activeShelf = $bindable() } = $props();
</script>

<button id="double-shelf" class="w-[88px] h-[153px] flex items-center justify-center cursor-pointer border-2 border-transparent {shelfName === 'A' ? 'hover:border-r-accent-300' : 'hover:border-l-accent-300'}" aria-label="Shelf on floor with name {shelfName}" onclick={() => {detailedShelfOpen = !detailedShelfOpen; activeShelf = shelfName;}}>
    <span class="font-title text-h3 text-grey-500"> {shelfName} </span>
</button>

<style>
    #double-shelf {
        background-image: url('/assets/TopDownLongShelves.svg');
        background-size: cover;
    }
</style>