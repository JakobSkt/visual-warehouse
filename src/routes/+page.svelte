<script lang="ts">
    import ActionsColumn from "$lib/components/ActionsColumn.svelte";
    import Floor from "$lib/components/Floor.svelte";
    import Receive from "$lib/components/Receive.svelte";
    import Ship from "$lib/components/Ship.svelte";
    import Navbar from "$lib/components/Navbar.svelte";
    import PalletTableView from "$lib/components/PalletTableView.svelte";
    import ModeSwitcher from "$lib/components/ModeSwitcher.svelte";
    import {onMount} from "svelte";
    import {userPrefersMode} from "mode-watcher";
    import {shortcuts} from "svelte-keyboard-shortcuts";
    import SideReceive from "$lib/components/SideReceive.svelte";
    import SideShip from "$lib/components/SideShip.svelte";

    type Sections = "floor" | "receive" | "ship"
    let activeSection: Sections = $state("floor");
    let borderColor = $state("border-grey-700");

    let mainSectionWidth = $state("");

    $effect(() => {
        /* Toggling border color of main section on mobile */
        if (activeSection === "floor") {
            borderColor = "border-grey-900";
        } else if (activeSection === "receive") {
            borderColor = "border-receive-700";
        } else {
            borderColor = "border-ship-700";
        }

        /* Calculating width of main section based on side panels state */
        if (receivePanelOpen || shipPanelOpen) {
            if (receivePanelOpen) {
                mainSectionWidth = "w-[42vw] float-right place-self-end mr-28";
            } else {
                mainSectionWidth = "w-[42vw] float-left place-self-start ml-28";
            }
        } else {
            mainSectionWidth = "w-[85vw]";
        }
    })

    let itemsToPlace = [
        {
            name: "Truck",
            description: "Use a truck to move pallets across your warehouse",
            img_url: "/assets/Truck.svg",
            shortcut: ['a', 't'],
        },
        {
            name: "Rack",
            description: "Use a rack to organize your warehouse both horizontally and vertically. Can directly store pallets.",
            img_url: "/assets/Shelves.svg",
            shortcut: ['a', 'r'],
        },
        {
            name: "Pallet",
            description: "Use a pallet to store your items on racks",
            img_url: "/assets/Pallet.svg",
            shortcut: ['a', 'p'],
        },
        {
            name: "Small pallet",
            description: "Use a small pallet to store your items on racks",
            img_url: "/assets/WeirdPallet.svg",
            shortcut: ['a', 's'],
        },
        {
            name: "Blue crates",
            description: "Use a pallet to store your items on racks",
            img_url: "/assets/BlueCrate.svg",
            shortcut: ['a', 'c'],
        },
        {
            name: "Plastic wrap",
            description: "Use plastic wrap to protect items on pallets or blue crates.",
            img_url: "/assets/PlasticWrap.svg",
            shortcut: ['a', 'w'],
        },
    ]

    let actionsColumnOpen: boolean = $state(false);
    let detailedShelfOpen: boolean = $state(false);
    let detailedPalletOpen: boolean = $state(false);

    let isDesktop = $state(false);
    let logoPath = $derived(userPrefersMode.current === "dark" ? "/assets/VisualWarehouseDark.svg" : "/assets/VisualWarehouse-light.svg");

    let receivePanelOpen = $state(false);
    let shipPanelOpen = $state(false);

    onMount(() => {
        isDesktop = window.innerWidth > 1024;
        window.addEventListener("resize", () => {
            isDesktop = window.innerWidth > 1024;
        });
    })

</script>

<div class="w-screen min-h-dvh lg:h-screen dark:bg-grey-900 bg-brand-500 flex flex-col items-center justify-start pt-10 overflow-hidden">
    <ModeSwitcher/>

    <header class="mx-12 mb-4" id="header">
        {#if isDesktop}
            <!-- *** DESKTOP HEADER + NAVBAR *** -->
            <nav class="flex w-[85vw] bg-brand-300 dark:bg-grey-700 px-6 py-4 rounded-default items-center justify-between">
                <button tabindex="0" use:shortcuts={{ keys: ['h'] }} onclick={() => window.location.reload()}
                        aria-label="Navigate home" class="cursor-pointer">
                    <img class="h-10" src="{logoPath}" alt="VisualWarehouse Logo">
                </button>
                <div class="flex items-center justify-center gap-4">
                    {#each itemsToPlace as item}
                        <button use:shortcuts={{ keys: item.shortcut }}
                                class="h-16 w-16 flex flex-col items-center justify-center gap-2 cursor-pointer hover:scale-105 transition-all"
                                aria-label="Place {item.name}" onclick={() => alert(`Place ${item.name}`)}>
                            <img class="w-full h-full {item.name === 'Truck' ? '-rotate-90' : ''}" src="{item.img_url}"
                                 alt="{item.description}">
                        </button>
                    {/each}
                </div>
            </nav>
        {:else}
            <!-- MOBILE HEADER; NAVBAR AT BOTTOM -->
            <button onclick={() => window.location.reload()} aria-label="Navigate home" class="cursor-pointer">
                <img src={logoPath} alt="VisualWarehouse Logo">
            </button>
        {/if}
    </header>

    <!-- SIDE PANELS ON DESKTOP -->
    {#if isDesktop}
        <SideReceive bind:open={receivePanelOpen} bind:oppositePanelOpen={shipPanelOpen} />
        <SideShip bind:open={shipPanelOpen} bind:oppositePanelOpen={receivePanelOpen} />
    {/if}

    <!-- *** MAIN SECTION START *** -->
    <main class="relative {mainSectionWidth} h-[60vh] lg:h-[80vh] flex flex-col items-center justify-center overflow-x-scroll overflow-y-hidden scrollbar-none border-default {borderColor} rounded-default"
          id="actions">
        {#if isDesktop}
            <!-- DESKTOP VIEW -->
            <Floor bind:detailedShelfOpen={detailedShelfOpen} bind:detailedPalletOpen={detailedPalletOpen} {isDesktop}/>
            {#if detailedPalletOpen}
                <PalletTableView bind:open={detailedPalletOpen} {isDesktop}/>
            {/if}

        {:else}
            <!-- MOBILE VIEW -->
            {#if activeSection === "floor"}
                {#if isDesktop}
                    <Floor bind:detailedShelfOpen={detailedShelfOpen} bind:detailedPalletOpen={detailedPalletOpen}
                           {isDesktop}/>
                    {#if detailedPalletOpen}
                        <PalletTableView bind:open={detailedPalletOpen} {isDesktop}/>
                    {/if}
                {:else}
                    {#if detailedPalletOpen}
                        <PalletTableView bind:open={detailedPalletOpen} {isDesktop}/>
                    {:else}
                        <Floor bind:detailedShelfOpen={detailedShelfOpen} bind:detailedPalletOpen={detailedPalletOpen}
                               {isDesktop}/>
                        <ActionsColumn open={actionsColumnOpen}/>
                    {/if}
                {/if}
            {:else if activeSection === "receive"}
                <Receive/>
            {:else}
                <Ship/>
            {/if}
        {/if}

    </main>
    <!-- *** MAIN SECTION END *** -->

    <!-- *** NAVBAR ON MOBILE *** -->
    {#if !isDesktop}
        <Navbar bind:activeSection={activeSection}/>
    {/if}
</div>