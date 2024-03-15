<script>
    export let type
</script>

{#if type == "brand"}
    <div class="mt-12 text-center print:hidden">
        <h1 class="text-5xl font-bold">Jaya Ma'mur Struk</h1>
        <h2 class="text-3xl text-blue-500 italic mt-2">Dibuat Oleh <span class="font-semibold">Micola Arighi</span></h2>
    </div>
{:else if type == "preview"}
    <div class="mt-12 text-center print:hidden">
        <h1 class="text-5xl font-bold">Preview Struk</h1>
        <h2 class="text-3xl text-blue-500 italic mt-2">Pastikan <span class="font-semibold">Info Benar!</span></h2>
    </div>
{/if}
