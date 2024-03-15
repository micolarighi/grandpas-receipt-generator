<script>
	import Header from '../components/Header.svelte';
	import ItemList from '../components/ItemList.svelte';
	import Button from '../components/Button.svelte';
	import Print from '../components/Print.svelte';
	import TableItem from '../components/TableItem.svelte';
	import Quantity from '../components/Quantity.svelte';
	import Receipt from '../components/Receipt.svelte';
	import Extra from '../components/Extra.svelte';
	import { onMount } from 'svelte';
	import { toast } from '@zerodevx/svelte-toast';
	let itemList = [
		{ name: 'Plat TOKO (254 x 394)', price: 12000 },
		{ name: 'Plat GTO (400 x 510)', price: 22000 },
		{ name: 'Plat SM (459 x 574)', price: 24000 },
		{ name: 'Plat Oliver 58 (508 x 570)', price: 35000 },
		{ name: 'Plat MO (550 x 650)', price: 42000 },
		{ name: 'Plat Komori (560 x 670)', price: 45000 },
		{ name: 'Plat Oliver 72 (605 x 724)', price: 55000 },
		{ name: 'Plat SM 72 ( 615 x 724)', price: 56000 },
		{ name: 'Film pos-neg(A4)', price: 32000 },
		{ name: 'Film pos-net(/cm)', price: 50 }
	];
	let currentSelectedItem = 0;
	let quantity = 1;
	let showReceipt = false;
	let receiptId;
	let towards = 'CASH';
	let addedItems = [];
	onMount(() => {
		receiptId = localStorage.getItem('receiptId');
		return () => {};
	});
	function handleChange(selectedItem) {
		currentSelectedItem = selectedItem.detail;
	}
	function handleQuantityChange(qtt) {
		quantity = qtt.detail;
	}
	function handleClick() {
		addedItems = [
			...addedItems,
			[
				itemList[currentSelectedItem].name,
				itemList[currentSelectedItem].price,
				quantity,
				parseInt(itemList[currentSelectedItem].price) * quantity
			]
		];
		toast.push('Barang berhasil ditambah!');
	}
	function handleShowReceipt() {
		if (addedItems.length >= 1 && receiptId != null && receiptId > 0) {
			showReceipt = !showReceipt;
		} else if (receiptId < 1 || receiptId == null) {
			toast.push('Nomor Nota tidak Valid!');
		} else {
			toast.push('Masukkin barang dulu bos!');
		}
	}
	function pad(num, size) {
		num = num.toString();
		while (num.length < size) num = '0' + num;
		return num;
	}
	function handlePrint(print) {
		if (print.detail) {
			showReceipt = !showReceipt;
			window.print();
			receiptId = parseInt(receiptId) + 1;
			localStorage.setItem('receiptId', receiptId);
		} else {
			showReceipt = !showReceipt;
		}
	}
	function handleReceiptDetail(e) {
		towards = e.detail[0];
		receiptId = e.detail[1];
	}
	function handleClear() {
		toast.push('Barang berhasil dihapus!');
		addedItems = [];
	}
</script>

{#if showReceipt}
	<Header type={'preview'} />
	<Receipt {addedItems} {receiptId} {towards} on:customClick={handlePrint} />
{:else}
	<Header type={'brand'} />
	<div class="grid py-12 px-20 gap-6 grid-cols-12">
		<div class="col-span-4 lg:col-span-3 border-2 border p-5 border-gray-600 rounded shadow-xl">
			<ItemList {itemList} on:change={handleChange} />
			<Quantity on:quantityChange={handleQuantityChange} />
			<Button on:customClick={handleClick} name="Tambah Barang" />
			<Button on:customClick={handleClear} name="Hapus Semua" />
		</div>
		<div class="col-span-4 lg:col-span-6 border p-5 border-2 border-gray-600 rounded shadow-xl">
			{#if addedItems.length <= 0}
				<div class="text-center flex justify-center h-full flex-col">
					<h1 class="text-5xl font-bold">Barang kosong!</h1>
					<h2 class="mt-2 text-xl text-gray-500 font-semibold">
						Tambahin barang buat mulai bikin struk
					</h2>
				</div>
			{:else}
				<div class="relative overflow-x-auto">
					<table class="w-full text-sm text-left text-gray-500">
						<thead class="text-xs text-gray-700 uppercase bg-gray-50">
							<tr>
								<th scope="col" class="px-6 py-3"> Nama Barang </th>
								<th scope="col" class="px-6 py-3"> Satuan Rp. </th>
								<th scope="col" class="px-6 py-3"> Qtt </th>
								<th scope="col" class="px-6 py-3"> Jumlah Rp. </th>
							</tr>
						</thead>
						<tbody>
							{#each addedItems as item, index}
								<TableItem item={[item]} />
							{/each}
						</tbody>
					</table>
				</div>
			{/if}
		</div>
		<div class="col-span-3 lg:col-span-3 border p-5 border-2 border-gray-600 rounded shadow-xl">
			<Extra {receiptId} on:change={handleReceiptDetail} />
			<div class="border border-b" />
			<Print />
			<Button on:customClick={handleShowReceipt} name="Print" />
		</div>
	</div>
{/if}
