<script>
    import '../app.css'
    import { SvelteToast } from '@zerodevx/svelte-toast'
</script>

<div class="flex flex-col justify-center h-[90vh] items-center">
    <slot/>
</div>

<div class="print:hidden">
    <SvelteToast/>
</div>

