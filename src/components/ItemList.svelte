<script>
    import {createEventDispatcher} from 'svelte'
    const dispatch = createEventDispatcher()
    export let itemList
    let selectedItem = 0
    function handleChange() {
        dispatch('change', selectedItem)
    }
</script>
<h1 class="text-2xl font-bold">Tambah Barang</h1>
<h3 class="mb-3 text-blue-500">Pilih barang dulu bos</h3>
<select bind:value={selectedItem} on:change={handleChange} size="8" class="focus:border focus:border-gray-600 focus:outline-none border border-gray-300 p-3 rounded w-full">
    {#each itemList as item, index}
    <option value={index}>{item.name}</option>
    {/each}
</select>