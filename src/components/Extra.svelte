<script>
    import {createEventDispatcher} from 'svelte'
    import {onMount} from "svelte";
    const dispatch = createEventDispatcher()
    let towards = 'CASH'
    export let receiptId
    function pad(num, size) {
        num = num.toString();
        while (num.length < size) num = "0" + num;
        return num;
    }
    function handleChange() {
        dispatch('change', [towards, pad(receiptId, 6)])
    }    
</script>
<div class="mb-3">
    <h1 class="text-2xl font-bold" >Nomor Nota :</h1>
    <h3 class="mb-3 text-blue-500 mb-3">Isi manual jika salah</h3>
    <input bind:value={receiptId} on:change={handleChange} type="text" class="border w-full border-gray-600 rounded px-2 py-1 focus:outline-none">
</div>
<div class="border border-b mb-4"></div>
<div>
    <h1 class="text-2xl font-bold mb-3">Kepada :</h1>
    <input bind:value={towards} on:change={handleChange} type="text" class="border w-full border-gray-600 rounded px-2 py-1 focus:outline-none">
</div>
<div class="mt-4">
</div>