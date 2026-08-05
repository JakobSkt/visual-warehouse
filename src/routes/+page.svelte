<script lang="ts">
    import ActionsColumn from "$lib/components/ActionsColumn.svelte";
    import DoubleShelf from "$lib/components/DoubleShelf.svelte";
    import Pallet from "$lib/components/Pallet.svelte";
    import DetailedShelf from "$lib/components/DetailedShelf.svelte";
    import Floor from "$lib/components/Floor.svelte";
    import Receive from "$lib/components/Receive.svelte";
    import Ship from "$lib/components/Ship.svelte";
    import Navbar from "$lib/components/Navbar.svelte";
    import PalletTableView from "$lib/components/PalletTableView.svelte";
    import {onMount} from "svelte";

    type Sections = "floor" | "receive" | "ship"
    let activeSection: Sections = $state("floor");
    let borderColor = $state("border-grey-700");
    $effect(() => {
        if (activeSection === "floor") {
            borderColor = "border-grey-900";
        } else if (activeSection === "receive") {
            borderColor = "border-receive-700";
        } else {
            borderColor = "border-ship-700";
        }
    })

    let itemsToPlace = [
        {name: "Truck", description: "Use a truck to move pallets across your warehouse", img_url: "/assets/Truck.svg"},
        {
            name: "Rack",
            description: "Use a rack to organize your warehouse both horizontally and vertically. Can directly store pallets.",
            img_url: "/assets/Shelves.svg"
        },
        {name: "Pallet", description: "Use a pallet to store your items on racks", img_url: "/assets/Pallet.svg"},
        {
            name: "Small pallet",
            description: "Use a small pallet to store your items on racks",
            img_url: "/assets/WeirdPallet.svg"
        },
        {
            name: "Blue crates",
            description: "Use a pallet to store your items on racks",
            img_url: "/assets/BlueCrate.svg"
        },
        {
            name: "Plastic wrap",
            description: "Use plastic wrap to protect items on pallets or blue crates.",
            img_url: "/assets/PlasticWrap.svg"
        },
    ]

    let actionsColumnOpen: boolean = $state(false);
    let detailedShelfOpen: boolean = $state(false);
    let detailedPalletOpen: boolean = $state(false);

    let isDesktop = $state(false)
    onMount(() => {
        isDesktop = window.innerWidth > 1024;
        window.addEventListener("resize", () => {
            isDesktop = window.innerWidth > 1024;
        });
    })

</script>

<div class="w-screen min-h-dvh lg:h-screen bg-brand-500 flex flex-col items-center justify-start pt-10 overflow-hidden">
    <header class="mx-12 mb-4" id="header">
        {#if isDesktop}
            <!-- *** Desktop header + navbar *** -->
            <nav class="flex w-[85vw] bg-brand-300 px-6 py-4 rounded-default items-center justify-between">
                <button onclick={() => window.location.reload()} aria-label="Navigate home" class="cursor-pointer">
                    <img src="/assets/VisualWarehouse.svg" alt="VisualWarehouse Logo">
                </button>
                <div class="flex items-center justify-center gap-4">
                    {#each itemsToPlace as item}
                        <button class="h-16 w-16 flex flex-col items-center justify-center gap-2 cursor-pointer hover:scale-105 transition-all"
                                aria-label="Place {item.name}" onclick={() => alert(`Place ${item.name}`)}>
                            <img class="w-full h-full {item.name === 'Truck' ? '-rotate-90' : ''}" src="{item.img_url}"
                                 alt="{item.description}">
                        </button>
                    {/each}
                </div>
            </nav>
        {:else}
            <button onclick={() => window.location.reload()} aria-label="Navigate home" class="cursor-pointer">
                <img src="/assets/VisualWarehouse.svg" alt="VisualWarehouse Logo">
            </button>
        {/if}
    </header>
    <main class="relative w-[85vw] h-[60vh] lg:h-[80vh] flex flex-col items-center justify-center overflow-x-scroll overflow-y-hidden scrollbar-none border-default {borderColor} rounded-default" id="actions">

        <!-- *** Main Section start *** -->
        {#if activeSection === "floor"}
            {#if isDesktop}
                <Floor bind:detailedShelfOpen={detailedShelfOpen} bind:detailedPalletOpen={detailedPalletOpen} {isDesktop} />
                {#if detailedPalletOpen}
                    <PalletTableView bind:open={detailedPalletOpen} {isDesktop} />
                {/if}
            {:else}
                {#if detailedPalletOpen}
                    <PalletTableView bind:open={detailedPalletOpen} {isDesktop} />
                {:else}
                    <Floor bind:detailedShelfOpen={detailedShelfOpen} bind:detailedPalletOpen={detailedPalletOpen} {isDesktop} />
                    <ActionsColumn open={actionsColumnOpen}/>
                {/if}
            {/if}

        {:else if activeSection === "receive"}
            <Receive/>
        {:else}
            <Ship/>
        {/if}
        <!-- *** Main Section end *** -->
    </main>
    <!-- *** Navbar showing on Mobile *** -->
    {#if !isDesktop}
        <Navbar bind:activeSection={activeSection}/>
    {/if}
</div>