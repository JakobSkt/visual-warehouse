<script lang="ts">
    import Pallet from "$lib/components/Pallet.svelte";
    import ActionsColumn from "$lib/components/ActionsColumn.svelte";
    import DetailedShelf from "$lib/components/DetailedShelf.svelte";
    import DoubleShelf from "$lib/components/DoubleShelf.svelte";

    let { detailedShelfOpen = $bindable() } = $props();
</script>

<div class="w-[120vw] h-[75vh] flex flex-row-reverse items-center justify-between bg-ship-500 p-2">
    SHIP
</div>

