<script>
    import {createEventDispatcher} from 'svelte'
    const dispatch = createEventDispatcher()
    export let name = ''
</script>

{#if name == "Hapus Semua"}
    <button on:click={ () => dispatch('customClick')} class="bg-red-500 hover:bg-red-700 px-3 py-2 mt-3 text-white rounded-md w-full">
        {name}
    </button>
{:else}
    <button on:click={ () => dispatch('customClick')} class="bg-blue-500 hover:bg-blue-700 px-3 py-2 mt-3 text-white rounded-md w-full">
        {name}
    </button>
{/if}
