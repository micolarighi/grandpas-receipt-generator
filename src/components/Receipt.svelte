<script>
	import { createEventDispatcher } from 'svelte';
	const dispatch = createEventDispatcher();
	import Logo from '$lib/assets/logo.png';
	export let receiptId;
	let d = new Date();
	let dayDate = d.getDate();
	let monthDate = d.getMonth();
	let yearDate = d.getFullYear();
	export let addedItems;
	export let towards;
	let total = 0;

	function pad(num, size) {
		num = num.toString();
		while (num.length < size) num = '0' + num;
		return num;
	}

	for (let index = 0; index < addedItems.length; index++) {
		total += addedItems[index][3];
	}
</script>

<div class="flex items-center print:mt-[-55vh] w-screen flex-col mt-8">
	<div id="receipt-container" class="outline p-[0.10in] m-0">
		<div class="grid grid-cols-12">
			<div class="col-span-1">
				<img src={Logo} alt="Logo" width="40px" class="mt-2" />
			</div>
			<div class="col-span-7 text-[10px] pl-1">
				<h1 class="text-[16px]">JAYA MA'MUR</h1>
				<h1 class="text-[12px]">JL. Otista 2 No. 67A Lantai 3 - Jakarta Timur</h1>
				<h1 class="text-[11px]">graphicrepro5jm@gmail.com</h1>
				<h1 class="text-[16px]">Telp.8190885</h1>
			</div>
			<div class="text-[16px] pl-2 col-span-4">
				{dayDate}/{monthDate + 1}/{yearDate}
				<h1 class="text-[14px] mt-3">Kepada:</h1>
				<p class="text-[18px] mt-2">{towards}</p>
			</div>
		</div>
				<h1 class="text-[18px] mx-1 mt-3 border border-black p-1 text-center">Nota No.{pad(receiptId, 6)}</h1>
		<div class="mt-4">
			<table>
				<thead>
					<tr>
						<th>Nama Barang</th>
						<th>Satuan <br /> Rp.</th>
						<th>Qtt</th>
						<th>Jumlah <br /> Rp.</th>
					</tr>
				</thead>
				<tbody>
					{#each addedItems as item}
						<tr>
							<td class="text-[12px] leading-[1.1]">{item[0]}</td>
							<td class="text-[15px]">{item[1]}</td>
							<td class="text-[15px]">{item[2]}</td>
							<td class="text-[15px]">{item[3]}</td>
						</tr>
					{/each}
				</tbody>
			</table>
		</div>
		<div class="mt-2 border-b-2 border-black mb-3" />
		<div class="flex justify-between">
			<h1>Total</h1>
			<h1>
				{total}
			</h1>
		</div>
	</div>
	<div class="mt-3 print:hidden">
		<div class="border border-b mt-3" />
		<h1 class="mt-5 mb-2 text-2xl">Yakin ingin print struk?</h1>
		<button
			on:click={() => dispatch('customClick', true)}
			class="bg-blue-500 w-full px-3 py-2 rounded text-white">Ya, Print!</button
		>
		<button
			on:click={() => dispatch('customClick', false)}
			class="bg-gray-500 w-full px-3 py-2 rounded text-white mt-3">Batal dulu</button
		>
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
		font-family: header;
		font-weight: 600;
		margin-bottom: 0 !important;
	}
	@media print {
		@page {
			margin: 0 !important;
			padding: 0 !important;
			height: 70mm;
		}
	}
	table {
		font-size: 75%;
		table-layout: fixed;
		width: 100%;
	}
	table {
		border-collapse: separate;
		border-spacing: 2px;
	}
	th,
	td {
		border-width: 1.3px;
		position: relative;
		text-align: center;
	}
	th,
	td {
		border-radius: 0.1em;
		border-style: solid;
		padding: 0.2em;
	}
	th {
		border-color: rgb(0, 0, 0);
	}
	td {
		border-color: rgb(0, 0, 0);
	}

	table th:nth-child(1) {
		width: 45%;
	}

	table th:nth-child(2) {
		width: 20%;
	}
	table th:nth-child(3) {
		width: 10%;
	}
	table th:nth-child(4) {
		width: 23%;
	}
</style>
