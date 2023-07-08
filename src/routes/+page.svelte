<script>
    import Header from '../components/Header.svelte'
    import ItemList from '../components/ItemList.svelte'
    import Button from '../components/Button.svelte'
    import Print from '../components/Print.svelte'
    import TableItem from '../components/TableItem.svelte'
    import Quantity from '../components/Quantity.svelte';
	import Receipt from '../components/Receipt.svelte';
    import Extra from '../components/Extra.svelte'
    let itemList = [{name : "Plat TOKO (254 x 394)", price: 12000}, {name : "Plat GTO (400 x 510)", price : 22000}, {name : "Plat SM (459 x 574)", price : 24000}, {name : "Plat Oliver 58 (508 x 570)", price : 35000}, {name : "Plat MO (550 x 650)", price : 42000}, {name : "Plat Komori (560 x 670)", price : 45000}, {name : "Plat Oliver 72 (605 x 724)", price : 55000}, {name : "Plat SM 72 ( 615 x 724)", price: 56000}, {name : "Film pos-neg(A4)", price: 32000}, {name : "Film pos-net(/cm)", price :50}]
    let currentSelectedItem = 0
    let quantity = 1
    let showReceipt = false
    function handleChange(selectedItem) {
        currentSelectedItem = selectedItem.detail
    }
    function handleQuantityChange (qtt) {
        quantity = qtt.detail
    }
    function handleClick() {
        addedItems = [...addedItems, [ (itemList[currentSelectedItem].name), (itemList[currentSelectedItem].price), quantity, (itemList[currentSelectedItem].price * quantity)]]
        console.log(addedItems)
    }
    function handleShowReceipt() {
        showReceipt = !showReceipt
    }

    function handlePrint(print) {
        if (print.detail){
            showReceipt = !showReceipt
            window.print()
        } else {
            showReceipt = !showReceipt
        }
    }
    let addedItems = []
</script>

<Header/>
{#if showReceipt}
    <Receipt on:customClick={handlePrint} />
{:else}
<div class="grid py-12 px-20 gap-6 grid-cols-12">
    <div class="col-span-3 border p-5 border-gray-600 rounded shadow-lg">
        <ItemList {itemList} on:change={handleChange} />
        <Quantity on:quantityChange={handleQuantityChange} />
        <Button on:customClick={handleClick} name="Tambah Barang"/>
        <div class="border border-b"></div>
        <Print/>
        <Button on:customClick={handleShowReceipt} name="Print" />
    </div>
    <div class="col-span-6 border p-5 border-gray-600 rounded shadow-lg">
        {#if addedItems.length <= 0} 
        <div class="text-center flex justify-center h-full flex-col">
            <h1 class="text-5xl text-gray-600">Barang  kosong!</h1>
            <h2 class="mt-2 text-xl text-blue-400">Tambahin barang buat mulai bikin struk</h2>
        </div>
        {:else}
        <div class="relative overflow-x-auto">
                <table class="w-full text-sm text-left text-gray-500">
                    <thead class="text-xs text-gray-700 uppercase bg-gray-50">
                        <tr>
                            <th scope="col" class="px-6 py-3">
                                Nama Barang
                            </th>
                            <th scope="col" class="px-6 py-3">
                                Satuan Rp.
                            </th>
                            <th scope="col" class="px-6 py-3">
                                Qtt
                            </th>
                            <th scope="col" class="px-6 py-3">
                                Jumlah Rp.
                            </th>
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
    <div class="col-span-3 border p-5 border-gray-600 rounded shadow-lg">
        <Extra/>
    </div>
</div>
{/if}

