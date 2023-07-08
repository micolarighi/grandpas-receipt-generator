<script>
    import {createEventDispatcher} from 'svelte'
    const dispatch = createEventDispatcher()
    let quantity = 1
    function handleIncrement () {
        quantity += 1
    }
    function handleDecrement () {
        if (quantity >= 2) {
            quantity -= 1
        }
    }

    $: {
        dispatch("quantityChange", quantity)
    }
</script>
<div class="grid grid-cols-3 mt-3 gap-2">
    <button on:click={handleDecrement} class="bg-neutral-500 rounded text-white py-2">-</button>
    <input bind:value={quantity} type="number" class="text-center focus:outline-none focus:border focus:border-neutral-500 rounded">
    <button on:click={handleIncrement} class="bg-neutral-500 rounded text-white py-2">+</button>
</div>