<script lang="ts">
    import ItemActionsPopup from "$lib/components/ItemActionsPopup.svelte";

    let {open = $bindable(false), isDesktop} = $props();
    let itemPopup: boolean = $state(false);
    let containerElement: HTMLElement;
    let popupPosition: { top: number, left: number } = $state({top: 0, left: 0});

    let sortingActive = $state(false);
    let sortingDirection: "asc" | "desc" = $state("asc");
    let sortingColumn: "qty" | "name" | "ean" = $state("qty"); // Placeholder value

    function openItemActionsPopup(e: MouseEvent) {
        const btn = e.currentTarget as HTMLButtonElement;
        const btnRect = btn.getBoundingClientRect();
        const containerRect = containerElement.getBoundingClientRect();

        popupPosition = {
            top: btnRect.top - containerRect.top,
            left: btnRect.left - containerRect.left - 20,
        };

        itemPopup = true;
    }

    function handlePopupClick(e: MouseEvent) {
        if (!e.target || !(e.target instanceof HTMLElement)) return;
        if (e.target.id !== "popupTrigger") {
            itemPopup = false;
        }
    }

    function onAddToShipment() {
        alert("Added to shipment");
        console.log("Added to shipment");
    }

    function onShowBarcode() {
        alert("Showed barcode");
        console.log("Showed barcode");
    }

    let exampleItems = $state([
        {qty: 1, name: "LG OLED55G66LW", ean: "519086197209"},
        {qty: 2, name: "SONY K-55XR80 AZ1", ean: "518051610812"},
        {qty: 2, name: "Panasonic PZ25810", ean: "406180180190"},
    ]);

    function toggleSorting(column: "qty" | "name" | "ean") {
        if (sortingActive && sortingColumn === column) {
            sortingDirection = sortingDirection === "asc" ? "desc" : "asc";
        } else {
            sortingActive = true;
            sortingColumn = column;
            sortingDirection = "asc";
        }

        exampleItems.sort((a, b) => {
            const valueA = a[column];
            const valueB = b[column];

            if (valueA < valueB) return sortingDirection === "asc" ? -1 : 1;
            if (valueA > valueB) return sortingDirection === "asc" ? 1 : -1;

            return 0;
        });
    }

</script>

<svelte:window onclick={handlePopupClick}/>

<div class="relative lg:absolute lg:bottom-[-2px] lg:left-0 w-full h-full lg:h-[50vh] lg:w-[50vw] lg:pl-8 lg:pt-8 lg:pb-8 flex flex-col lg:flex-row-reverse items-center lg:items-start justify-start bg-brand-500 dark:bg-grey-500 border-2 border-grey-900 rounded-default overflow-clip z-50"
     bind:this={containerElement}>
    <div class="w-full lg:w-12 flex flex-row lg:flex-col items-center justify-end lg:justify-between lg:px-8 gap-2">
        <button class="m-0 p-0 flex flex-col float-right cursor-pointer group" aria-label="Close detailed pallet view"
                onclick={() => open = false}>
            <svg xmlns="http://www.w3.org/2000/svg" width="48" height="48" viewBox="0 0 24 24" fill="none"
                 stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                 class="lucide lucide-x-icon lucide-x stroke-grey-900 group-hover:stroke-grey-500 dark:stroke-brand-500 dark:hover:stroke-brand-100">
                <path d="M18 6 6 18"/>
                <path d="m6 6 12 12"/>
            </svg>
        </button>
        {#if isDesktop}
            <button class="m-0 p-0 flex flex-col cursor-pointer group" aria-label="Move detailed pallet view"
                    onclick={() => alert("Moved detailed pallet view")}>
                <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" viewBox="0 0 24 24" fill="none"
                     stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                     class="lucide lucide-move-icon lucide-move stroke-grey-900 group-hover:stroke-grey-500 dark:stroke-brand-500 dark:hover:stroke-brand-100">
                    <path d="M12 2v20"/>
                    <path d="m15 19-3 3-3-3"/>
                    <path d="m19 9 3 3-3 3"/>
                    <path d="M2 12h20"/>
                    <path d="m5 9-3 3 3 3"/>
                    <path d="m9 5 3-3 3 3"/>
                </svg>
            </button>
            <button class="m-0 p-0 flex flex-col cursor-pointer group" aria-label="Move detailed pallet view"
                    onclick={() => alert("3D detailed pallet view")}>
                <svg xmlns="http://www.w3.org/2000/svg" width="36" height="36" viewBox="0 0 24 24" fill="none"
                     stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
                     class="lucide lucide-rotate3d-icon lucide-rotate-3d stroke-grey-900 group-hover:stroke-grey-500 dark:stroke-brand-500 dark:hover:stroke-brand-100">
                    <path d="m15.194 13.707 3.814 1.86-1.86 3.814"/>
                    <path d="M16.47214 7.52786 A 5 10 0 1 0 13 21.79796"/>
                    <path d="M21.79796 11 A 10 5 0 1 0 19 15.57071"/>
                </svg>
            </button>
        {/if}
    </div>

    <!-- Item Actions pop-up -->
    {#if itemPopup}
        <ItemActionsPopup bind:open={itemPopup} {onAddToShipment} {onShowBarcode} top={popupPosition.top}
                          left={popupPosition.left}/>
    {/if}

    <table class="w-full h-full overflow-hidden lg:rounded-default">
        <thead class="bg-brand-100 dark:bg-grey-700">
        <tr>
            <th class="relative h-4">
                <button class="text-center" onclick={() => toggleSorting('qty')}> Qty </button>
                {#if sortingActive && sortingColumn === 'qty'}
                    {#if sortingDirection === 'asc'}
                        <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="absolute top-4 right-2 lucide lucide-chevron-down-icon lucide-chevron-down stroke-grey-700 dark:stroke-grey-300"><path d="m6 9 6 6 6-6"/></svg>
                    {:else}
                        <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="absolute top-4 right-2 lucide lucide-chevron-up-icon lucide-chevron-up stroke-grey-700 dark:stroke-grey-300"><path d="m18 15-6-6-6 6"/></svg>
                    {/if}
                {/if}
            </th>
            <th class="relative h-4">
                <button class="text-center" onclick={() => toggleSorting('name')}> Name </button>
                {#if sortingActive && sortingColumn === 'name'}
                    {#if sortingDirection === 'asc'}
                        <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="absolute top-4 right-2 lucide lucide-chevron-down-icon lucide-chevron-down stroke-grey-700 dark:stroke-grey-300"><path d="m6 9 6 6 6-6"/></svg>
                    {:else}
                        <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="absolute top-4 right-2 lucide lucide-chevron-up-icon lucide-chevron-up stroke-grey-700 dark:stroke-grey-300"><path d="m18 15-6-6-6 6"/></svg>
                    {/if}
                {/if}
            </th>
            <th class="relative h-4">
                <button class="text-center" onclick={() => toggleSorting('ean')}> EAN </button>
                {#if sortingActive && sortingColumn === 'ean'}
                    {#if sortingDirection === 'asc'}
                        <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="absolute top-4 right-2 lucide lucide-chevron-down-icon lucide-chevron-down stroke-grey-700 dark:stroke-grey-300"><path d="m6 9 6 6 6-6"/></svg>
                    {:else}
                        <svg xmlns="http://www.w3.org/2000/svg" width="10" height="10" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="absolute top-4 right-2 lucide lucide-chevron-up-icon lucide-chevron-up stroke-grey-700 dark:stroke-grey-300"><path d="m18 15-6-6-6 6"/></svg>
                    {/if}
                {/if}
            </th>
            <th class="lg:text-center"> {isDesktop ? 'Actions' : ''} </th>
        </tr>
        </thead>
        <tbody>
        {#each exampleItems as item, i}
            <tr>
                <td class="text-center"> {item.qty} </td>
                <td class="lg:text-center"> {item.name} </td>
                <td class="lg:text-center flex h-[51px] items-center justify-center gap-2">
                    {item.ean}
                    {#if isDesktop}
                        <button class="flex items-center justify-start cursor-pointer group" aria-label="Copy EAN"
                                onclick={() => {navigator.clipboard.writeText(item.ean); alert("Copied EAN to clipboard");}}>
                            <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24"
                                 fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                 stroke-linejoin="round"
                                 class="lucide lucide-copy-icon lucide-copy stroke-grey-700 group-hover:stroke-grey-500">
                                <rect width="14" height="14" x="8" y="8" rx="2" ry="2"/>
                                <path d="M4 16c-1.1 0-2-.9-2-2V4c0-1.1.9-2 2-2h10c1.1 0 2 .9 2 2"/>
                            </svg>
                        </button>
                    {/if}
                </td>
                <td class="lg:text-center">
                    {#if isDesktop}
                        <div class="flex flex-row items-center justify-center gap-2">
                            <button aria-label="Show EAN barcode" onclick={onShowBarcode}
                                    class="flex gap-2 items-center justify-start cursor-pointer group">
                                <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24"
                                     fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                     stroke-linejoin="round"
                                     class="lucide lucide-qr-code-icon lucide-qr-code stroke-grey-700 group-hover:stroke-grey-500 dark:stroke-grey-300">
                                    <rect width="5" height="5" x="3" y="3" rx="1"/>
                                    <rect width="5" height="5" x="16" y="3" rx="1"/>
                                    <rect width="5" height="5" x="3" y="16" rx="1"/>
                                    <path d="M21 16h-3a2 2 0 0 0-2 2v3"/>
                                    <path d="M21 21v.01"/>
                                    <path d="M12 7v3a2 2 0 0 1-2 2H7"/>
                                    <path d="M3 12h.01"/>
                                    <path d="M12 3h.01"/>
                                    <path d="M12 16v.01"/>
                                    <path d="M16 12h1"/>
                                    <path d="M21 12v.01"/>
                                    <path d="M12 21v-1"/>
                                </svg>
                            </button>
                            <button aria-label="Add to shipment" onclick={onAddToShipment}
                                    class="flex gap-2 items-center justify-start cursor-pointer group">
                                <svg xmlns="http://www.w3.org/2000/svg" width="28" height="28" viewBox="0 0 24 24"
                                     fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"
                                     stroke-linejoin="round"
                                     class="lucide lucide-truck-icon lucide-truck stroke-grey-700 group-hover:stroke-grey-500 dark:stroke-grey-300">
                                    <path d="M14 18V6a2 2 0 0 0-2-2H4a2 2 0 0 0-2 2v11a1 1 0 0 0 1 1h2"/>
                                    <path d="M15 18H9"/>
                                    <path d="M19 18h2a1 1 0 0 0 1-1v-3.65a1 1 0 0 0-.22-.624l-3.48-4.35A1 1 0 0 0 17.52 8H14"/>
                                    <circle cx="17" cy="18" r="2"/>
                                    <circle cx="7" cy="18" r="2"/>
                                </svg>
                            </button>

                        </div>
                    {:else}
                        <button aria-label="Toggle item actions" onclick={openItemActionsPopup} class="cursor-pointer">
                            <svg id="popupTrigger" xmlns="http://www.w3.org/2000/svg" width="24" height="24"
                                 viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5"
                                 stroke-linecap="round" stroke-linejoin="round"
                                 class="lucide lucide-ellipsis-vertical-icon lucide-ellipsis-vertical stroke-grey-700 dark:stroke-grey-300">
                                <circle cx="12" cy="12" r="1"/>
                                <circle cx="12" cy="5" r="1"/>
                                <circle cx="12" cy="19" r="1"/>
                            </svg>
                        </button>
                    {/if}
                </td>
            </tr>
        {/each}
        {#each Array(6).fill(0) as _, i}
            <tr>
                <td></td>
                <td></td>
                <td></td>
                <td></td>
            </tr>
        {/each}
        </tbody>
    </table>
</div>

<style>
    table {
        border-collapse: separate;
        border-spacing: 0;
        overflow: hidden;
    }

    thead tr th {
        padding: 0.4rem 0.5rem;
    }

    table tr td {
        padding: 0.2rem 0.2rem;
        height: 40px;
    }

    tbody tr {
        background-color: var(--color-brand-300);
    }

    tbody tr td {
        border-top: 2px solid var(--color-brand-100);
    }

    @media (min-width: 1024px) {
        tbody tr td {
            border-right: 2px solid var(--color-brand-100);
        }
    }

    :global(.dark) tbody tr {
        background-color: var(--color-grey-700);
    }

    :global(.dark) tbody tr td {
        border-top: 2px solid var(--color-grey-500);
    }

    @media (min-width: 1024px) {
        :global(.dark) tbody tr td {
            border-right: 2px solid var(--color-grey-500);
        }
    }
</style>