<script>
	import {createEventDispatcher} from 'svelte'
	const dispatch = createEventDispatcher()
	import Logo from "$lib/assets/logo.png"
	export let receiptId
	let d = new Date();
	let dayDate = d.getDate()
	let monthDate = d.getMonth()
	let yearDate = d.getFullYear()
</script>
<div class="flex justify-center items-center w-screen flex-col mt-8">
	<div id="receipt-container" class="outline p-[0.15in]">
		<div class="grid grid-cols-12">
			<div class="col-span-1">
				<img src={Logo} alt="Logo" width="40px" class="mt-2">
			</div>
			<div class="col-span-7 text-[10px] pl-1">
				<h1 class="text-[15px]">JAYA MA'MUR</h1>
				<h1>JL. Otista 2 No. 67A Lantai 3</h1>
				<h1>Telp.8190665 - Jakarta Timur</h1>
				<h1>Email : graphicrepro5jm@gmail.com</h1>
				<h1 class="text-[14px] mt-3">Nota No.{receiptId}</h1>
			</div>
			<div class="text-[14px] pl-2">
				{dayDate}/{monthDate + 1}/{yearDate}
				<h1 class="text-[10px] mt-3">Kepada:</h1>
				<h1 class="text-[15px] mt-2">CASH</h1>
			</div>
		</div>
	</div>
	<div class="mt-3 print:hidden">
		<div class="border border-b mt-3"></div>
		<h1 class="mt-5 mb-2 text-2xl">Yakin ingin print struk?</h1>
		<button on:click={() => dispatch('customClick', true)} class="bg-blue-500 w-full px-3 py-2 rounded text-white">Ya, Print!</button>
		<button on:click={() => dispatch('customClick', false)} class="bg-gray-500 w-full px-3 py-2 rounded text-white mt-3">Batal dulu</button>

	</div>
</div>

<style>
	@font-face {
	font-family: header;
	src: url(../lib/assets/fonts/HATTEN.TTF);
	font-family: text;
	src: url(../lib/assets/fonts/MinionPro-Bold.otf);
  	}
	#receipt-container {
		min-width: 70mm;
		max-width: 70mm;
		min-height: 70mm;
		font-family: header;
		font-weight: bold;
	}
	@media print {
		@page { margin: 0; }
	}
</style>