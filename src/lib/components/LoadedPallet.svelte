<script lang="ts">
    let { detailedPalletView = $bindable() } = $props();
</script>

<button class="absolute bottom-[18vh] lg:bottom-[39.8vh] right-[18vw] lg:right-[19vw] w-20 h-20 lg:w-24 lg:h-24 border-2 border-transparent hover:border-accent-300 transition cursor-pointer" onclick={() => detailedPalletView = true}>
    <img src="/assets/PalletWithTVs.svg" alt="Pallet with TVs" class="w-full h-full">
</button>