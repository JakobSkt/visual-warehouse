<script lang="ts">
    import Pallet from "$lib/components/Pallet.svelte";
    import ActionsColumn from "$lib/components/ActionsColumn.svelte";
    import DetailedShelf from "$lib/components/DetailedShelf.svelte";
    import DoubleShelf from "$lib/components/DoubleShelf.svelte";
    import {onMount} from "svelte";

    let activeShelf = $state('A');

    let { detailedShelfOpen = $bindable(false), detailedPalletOpen = $bindable(false), isDesktop } = $props();

</script>

<div class="relative w-[120vw] h-[60vh] lg:w-[85vw] lg:h-[90vh] flex flex-row items-center justify-between bg-grey-700 overflow-hidden">
    {#if isDesktop}
        {#if detailedShelfOpen}
            <DetailedShelf bind:open={detailedShelfOpen} shelfName={activeShelf} bind:detailedPalletOpen />
        {/if}
            <div class="lg:scale-125 ml-12 lg:ml-0 p-8">
                <DoubleShelf bind:detailedShelfOpen shelfName={'A'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'A'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'A'} bind:activeShelf/>
            </div>
            <div class="scale-50 lg:scale-75 hidden lg:flex flex-col">
                <Pallet/>
                <Pallet/>
                <Pallet/>
            </div>
            <div class="lg:scale-125 ml-24 lg:mr-10">
                <DoubleShelf bind:detailedShelfOpen shelfName={'B'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'B'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'B'} bind:activeShelf/>
            </div>
    {:else}
        {#if detailedShelfOpen}
            <DetailedShelf bind:open={detailedShelfOpen} shelfName={activeShelf} bind:detailedPalletOpen />
        {:else}
            <div class="lg:scale-125 ml-12 lg:ml-0 p-8">
                <DoubleShelf bind:detailedShelfOpen shelfName={'A'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'A'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'A'} bind:activeShelf/>
            </div>
            <div class="scale-50 lg:scale-75 hidden lg:flex flex-col">
                <Pallet/>
                <Pallet/>
                <Pallet/>
            </div>
            <div class="lg:scale-125 ml-24 lg:mr-10">
                <DoubleShelf bind:detailedShelfOpen shelfName={'B'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'B'} bind:activeShelf/>
                <DoubleShelf bind:detailedShelfOpen shelfName={'B'} bind:activeShelf/>
            </div>

        {/if}
    {/if}
</div>

