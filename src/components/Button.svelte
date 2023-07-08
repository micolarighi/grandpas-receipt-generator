<script>
    import {createEventDispatcher} from 'svelte'
    const dispatch = createEventDispatcher()
    export let name = ''
</script>
<button on:click={ () => dispatch('customClick')} class="bg-blue-500 hover:bg-blue-700 px-3 py-2 my-3 text-white rounded-md w-full">
    {name}
</button>