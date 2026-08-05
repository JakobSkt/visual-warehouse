<script lang="ts">
    let { activeSection = $bindable() } = $props();
</script>

<nav class="w-[85vw] h-[8vh] lg:hidden flex flex-row bg-brand-300 dark:bg-grey-700 rounded-default p-2 absolute bottom-10">
    <button class="w-1/3 {activeSection === 'receive' ? 'bg-receive-300' : 'bg-receive-500'} flex flex-col items-center justify-center gap-0 rounded-l-small" onclick={() => activeSection = "receive"}>
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-scan-barcode-icon lucide-scan-barcode stroke-grey-900">
            <path d="M3 7V5a2 2 0 0 1 2-2h2"/><path d="M17 3h2a2 2 0 0 1 2 2v2"/><path d="M21 17v2a2 2 0 0 1-2 2h-2"/><path d="M7 21H5a2 2 0 0 1-2-2v-2"/><path d="M8 7v10"/><path d="M12 7v10"/><path d="M17 7v10"/>
        </svg>
        <span class="font-text text-p text-grey-900"> Receive </span>
    </button>
    <button class="w-1/3 {activeSection === 'floor' ? 'bg-grey-500' : 'bg-grey-700 dark:bg-grey-900'} flex flex-col items-center justify-center gap-0" onclick={() => activeSection = "floor"}>
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-warehouse-icon lucide-warehouse stroke-grey-300">
            <path d="M18 21V10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1v11"/><path d="M22 19a2 2 0 0 1-2 2H4a2 2 0 0 1-2-2V8a2 2 0 0 1 1.132-1.803l7.95-3.974a2 2 0 0 1 1.837 0l7.948 3.974A2 2 0 0 1 22 8z"/><path d="M6 13h12"/><path d="M6 17h12"/>
        </svg>
        <span class="font-text text-p text-grey-300"> Floor </span>
    </button>
    <button class="w-1/3 {activeSection === 'ship' ? 'bg-ship-300' : 'bg-ship-500'} flex flex-col items-center justify-center gap-0 rounded-r-small" onclick={() => activeSection = "ship"}>
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round" class="lucide lucide-truck-icon lucide-truck stroke-grey-100">
            <path d="M14 18V6a2 2 0 0 0-2-2H4a2 2 0 0 0-2 2v11a1 1 0 0 0 1 1h2"/><path d="M15 18H9"/><path d="M19 18h2a1 1 0 0 0 1-1v-3.65a1 1 0 0 0-.22-.624l-3.48-4.35A1 1 0 0 0 17.52 8H14"/><circle cx="17" cy="18" r="2"/><circle cx="7" cy="18" r="2"/>
        </svg>
        <span class="font-text text-p text-grey-100"> Ship </span>
    </button>

</nav>