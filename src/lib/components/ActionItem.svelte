<script lang="ts">
    let { name, description, img_url } = $props();
</script>

<button aria-label={name + " " + description} class="cursor-pointer" onclick={() => alert('Placed new ' + name)}>
    <img src={img_url} alt={description} class="w-12 h-12"/>
</button>

