
<template>
    <section class="mx-20">
        <div class="pt-24 pb-4">
                <NuxtLink onclick="window.history.go(-1); return false;">
                    <button class="bg-red-500 hover:bg-red-500 hover:text-red-900 font-bold py-2 px-9 rounded focus:outline-none focus:shadow-outline" type="button">
                    Kembali
                    </button>
                </NuxtLink>
        </div>
        <div class="flex sm:justify-between gap-10 justify-center h-fit w-full mt-4 px-2 duration-1000 ">
            <div class="flex flex-col w-full h-fit duration-1000">
                <div class="flex justify-between items-center duration-1000">
                    <h1 class="text-4xl font-semibold">Keranjang Saya</h1>
                    <h1 class="text-xl text-white bg-red-500 rounded px-2 py-2 font-semibold cursor-pointer hover:text-red-800 active:scale-95 duration-100" v-show="cartData.length > 0" @click="DeleteAll = true">Delete All</h1>
                </div>
                <div class="flex flex-col justify-center items-center h-80 text-xl text-gray-600 " v-show="cartData.length === 0">
                    <div>
                    Belum ada item
                    </div>
                    <div class="mt-2 hover:scale-110 hover:text-red-900 duration-1000 text-red-500 font-bold">
                        <NuxtLink to="/list">
                            Tambahkan item
                        </NuxtLink>
                    </div>
                </div>

                <div class="flex flex-col mt-5 mb-5 duration-1000">
                    <div class="flex flex-col py-3" v-for="cartProduct in cartData">
                        <div class="flex">
                            <div class="flex">
                                <NuxtLink :to="'/list/'+cartProduct.id">
                                <img :src="cartProduct.thumbnail" alt="" class="h-[188px] object-cover aspect-square">
                                </NuxtLink>
                                <div class="flex flex-col mx-6">
                                    <div class="flex w-full justify-between">
                                        <NuxtLink :to="'/list/'+cartProduct.id">
                                            <h2 class="">{{ cartProduct.title }}</h2>
                                        </NuxtLink>
                                    </div>
                                    <div class="flex items-center">
                                        <span class="font-semibold">${{ cartProduct.price }}</span>
                                    </div>
                                    <div class="flex items-center">
                                        <span class="flex items-center h-8 border shadow-lg hover:scale-105 active:scale-95 cursor-pointer rounded-tl-lg text-xl text-center px-4" @click="accumulateQty(cartProduct.id, -1, cartProduct.stock)">-</span>
                                        <input type="number" id="qty" class="text-slate-800 font-semibold text-center px-4 w-20" v-model="cartProduct.qty" min="1" :max="cartProduct.stock"/>
                                        <span class="flex items-center h-8 border shadow-lg hover:scale-105 active:scale-95 cursor-pointer rounded-tr-lg text-xl text-center px-4" @click="accumulateQty(cartProduct.id, 1, cartProduct.stock)">+</span>
                                        <span class="font-semibold ml-5">Stock : {{ cartProduct.stock-cartProduct.qty }}</span>
                                    </div>
                                    <div class="flex items-center">
                                        <span class="font-semibold pt-2 pb-2">Total : ${{ cartProduct.price*cartProduct.qty }}</span>
                                    </div>
                                    <div class="flex">
                                    <span class="text-white bg-rose-500 rounded px-1 py-1 font-semibold cursor-pointer hover:text-rose-800 active:scale-95 duration-100" @click="Delete1 = true">Delete</span>
                                    </div>
                                </div>
                            </div>
                        </div>
                        
                        <Transition>
                            <div class="flex fixed top-0 right-0 justify-center items-center w-screen h-screen z-[999]"
                                v-show="Delete1 === true">
                                <div class="flex absolute h-screen w-screen top-0 right-0 bg-slate-800 opacity-50 z-[1]"
                                    @click="Delete1 = false">
                                </div>
                                <div class="flex flex-col justify-between w-[600px] h-54 rounded-lg p-8 bg-white z-[2]">
                                    <div class="flex justify-end">
                                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="black" class="w-6 h-6 hover:cursor-pointer mt-1" @click="Delete1 = false">
                                            <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                                        </svg>
                                    </div>
                                    <div class="flex flex-col justify-center items-center text-lg mb-7">
                                        <div class="flex flex-col justify-center items-center pt-7">
                                            Yakin Ingin Menghapus Item Ini?
                                            <div class="flex mt-8">
                                                <img :src="cartProduct.thumbnail" alt="" class="h-[300px] object-cover aspect-square mx-1">
                                                <div class="flex flex-col mx-10">
                                                    <div class="flex w-full justify-between">
                                                            <h2 class="active:scale-95 duration-300">{{ cartProduct.title }}</h2>
                                                    </div>
                                                    <div class="flex items-center">
                                                        <span class="font-semibold">${{ cartProduct.price }}</span>
                                                    </div>
                                                </div>
                                            </div>
                                        </div>
                                    </div>
                                    <div class="flex justify-end">
                                        <div class="flex gap-5">
                                            <div class="text-rose-500 hover:scale-105 active:scale-95 font-medium cursor-pointer"
                                                @click="Delete1 = false">
                                                Tidak
                                            </div>
                                            <div class="text-slate-700 hover:scale-105 active:scale-95 font-medium cursor-pointer"
                                                @click="delete1(cartProduct.id), Delete1 = false">
                                                Ya
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </Transition>
                    </div>
                </div>
            </div>

            <div class="lg:flex justify-end w-full px-3 duration-1000 ">
                <div class="flex bg-white rounded-lg h-fit shadow-lg border w-96 sticky top-0 p-4 py-6">
                    <div class="flex flex-col gap-4 w-full">
                        <div class="flex flex-col pb-2 border-b border-slate-300">
                            <h1 class="text-center font-semibold text-slate-950 py-0">Summary</h1>   
                        </div>
                        <div class="flex justify-start mx-0">
                            <p class="font-bold">Item Yang Dipilih</p>
                        </div>
                        <div class="flex flex-col py-1" v-for="cartProduct in cartData">
                            <div class="flex">
                                <div class="flex">
                                    <div class="flex flex-col mx-1">
                                        <div class="flex w-full justify-between">
                                            <NuxtLink :to="'/list/'+cartProduct.id">
                                                <h2 class="active:scale-95 duration-300">{{ cartProduct.title }}</h2>
                                            </NuxtLink>
                                        </div>
                                        <div class="flex items-center">
                                            <span class="font-semibold">${{ cartProduct.price }}</span>
                                        </div>
                                        <div class="flex items-center">
                                            <span class="font-semibold">Qty : <input type="number" id="qty" class="text-slate-800 font-semibold text-start px-4 w-20" v-model="cartProduct.qty" disabled/></span>
                                        </div>
                                        <div class="flex items-center">
                                            <span class="font-bold">Total : ${{ cartProduct.price*cartProduct.qty }}</span>
                                        </div>
                                        <div class="flex">
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <p class="text-slate-600 font-bold pb-2" v-show="cartData.length > 0">Total Harga : ${{ (allPrice) }}</p>
                        <button class="bg-red-500 hover:bg-red-700 text-white text-xl font-bold py-2 px-4" v-show="cartData.length > 0" @click="Sum = true">
                            Check Out
                        </button>
                    </div>
                </div>
            </div>
        </div>        
    </section>
    
    <Transition>
        <div class="flex fixed top-0 right-0 justify-center items-center w-screen h-screen z-[999]"
            v-show="DeleteAll === true">
            <div class="flex absolute h-screen w-screen top-0 right-0 bg-slate-800 opacity-50 z-[2]"
                @click="DeleteAll = false">
            </div>
            <div class="flex flex-col justify-between w-[600px] h-74 rounded-lg p-8 bg-white z-[2]">
                <div class="flex justify-end">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="black" class="w-6 h-6 hover:cursor-pointer mt-1" @click="DeleteAll = false">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                    </svg>
                </div>
                <div class="flex flex-col justify-center items-center text-lg mb-8">
                    <div class="flex flex-col mx-8">
                        Semua Item Akan Di Hapus?
                    </div>
                </div>
                <div class="flex justify-end">
                    <div class="flex gap-5">
                        <div class="text-rose-500 hover:scale-105 active:scale-95 font-medium cursor-pointer"
                            @click="DeleteAll = false">
                            Tidak
                        </div>
                        <div class="text-slate-700 hover:scale-105 active:scale-95 font-medium cursor-pointer"
                            @click="deleteAll()">
                            Ya
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </Transition>

    <Transition>
        <div class="flex fixed top-0 right-0 justify-center items-center w-screen h-screen z-[999]"
            v-show="Sum === true">
            <div class="flex absolute h-screen w-screen top-0 right-0 bg-slate-800 opacity-70 z-[1]"
                @click="Sum = false">
            </div>
            <div class="flex flex-col justify-between w-[500px] h-[750px] rounded-lg p-5 bg-white z-[2]">
                <div class="flex justify-end">
                    <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="black" class="w-6 h-6 hover:cursor-pointer mt-1" @click="Sum = false">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                            </svg>
                </div>
                <div class="flex justify-center">
                        <p class="font-bold text-xl">Summary</p>
                </div>
                <div class="overflow-y-scroll">
                    <div class="flex flex-col mt-5 mb-5 duration-1000">
                        <div class="flex justify-start mx-2">
                        <p class="font-bold pb-5">Item Yang Dipilih</p>
                        </div>
                        <div class="flex flex-col py-2" v-for="cartProduct in cartData">
                            <div class="flex">
                                <div class="flex">
                                    <img :src="cartProduct.thumbnail" alt="" class="h-[128px] object-cover aspect-square mx-1">
                                    <div class="flex flex-col mx-6">
                                        <div class="flex w-full justify-between">
                                            <NuxtLink :to="'/list/'+cartProduct.id">
                                                <h2 class="active:scale-95 duration-300">{{ cartProduct.title }}</h2>
                                            </NuxtLink>
                                        </div>
                                        <div class="flex items-center">
                                            <span class="font-semibold">${{ cartProduct.price }}</span>
                                        </div>
                                        <div class="flex items-center">
                                            <span class="font-semibold">Qty : <input type="number" id="qty" class="text-slate-800 font-semibold text-start px-4 w-20" v-model="cartProduct.qty" disabled/></span>
                                        </div>
                                        <div class="flex items-center">
                                            <span class="font-bold">Total : ${{ cartProduct.price*cartProduct.qty }}</span>
                                        </div>
                                        <div class="flex">
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <label class="block text-gray-700 text-sm font-bold mb-2">
                        Nama Pemesan
                    </label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Nama">
                    <label class="pt-2 block text-gray-700 text-sm font-bold mb-2">
                        Nomor Telepon
                    </label>
                    <form>
                        <div class="grid rounded-xl overflow-hidden border border-gray-300">
                            <select class="outline-0 border-b border-gray-300 p-3">
                            <option value="+62" class="p-3">Indonesia (+62)</option>
                            </select>
                            <div class="p-0.5 relative form-input group">
                                <input class="outline-0 p-3 w-full focus:outline-1 focus:rounded-lg relative bg-transparent z-40"/>
                                <span class="absolute top-[50%] -translate-y-[50%] left-4 text-lg text-gray-500 z-30 group-hover:top-4 group-hover:text-sm transition-all ease">Nomor Telepon</span>
                            </div>
                        </div>
                    </form>
                    <label class="block text-gray-700 text-sm font-bold mb-2 mt-2">
                        Metode Pembayaran
                    </label>
                    <select name="" id="" class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline">
                        <option>-- PILIH --</option>
                        <option>COD (Bayar di Tempat)</option>
                        <option>Transfer Bank</option>
                        <option>Kartu Kredit/Debit</option>
                        <option>PayLater</option>
                    </select>
                    <label class="block text-gray-700 text-sm font-bold mb-2 mt-2">
                        Alamat
                    </label>
                    <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Alamat" cols="15" rows="5"></textarea>
                </div>
                <div class="flex justify-center mb-2 pt-5">
                        <p class="text-slate-600 font-bold">Total Bayar : ${{ (allPrice) }}</p>
                </div>
                <div class="flex justify-end">
                    <button class="bg-red-500 hover:bg-red-700 text-white text-xs font-bold py-2 px-4" @click="Thx = true">
                        Konfirmasi
                    </button>
                </div>
            </div>
        </div>
    </Transition>

    <Transition>
        <div class="flex fixed top-0 right-0 justify-center items-center w-screen h-screen z-[999]" v-show="Thx === true">
            <NuxtLink to="/list">
                <div class="flex absolute h-screen w-screen top-0 right-0 bg-slate-800 opacity-50 z-[1]"
                    @click="Thx = false, deleteAll()">
                </div>
            </NuxtLink>
            <div class="flex flex-col justify-between w-[600px] h-32 rounded-lg p-4 bg-white z-[2]">
                <div class="flex justify-end">
                    <NuxtLink to="/list">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="black" class="w-6 h-6 hover:cursor-pointer mt-1" @click="Thx = false, Sum = false, deleteAll()">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                    </NuxtLink>
                </div>
                <div class="flex flex-col justify-center items-center text-lg mb-8">
                    <div class="flex flex-col mx-8">
                        Pesanan akan segera di proses, Terimakasih Telah Berbelanja!
                    </div>
                </div>
            </div>
        </div>
    </Transition>
</template>

<script>
export default {
data() {
    return {
        cartData: [],
        allPrice: 0,
        allQty: 0,
        Delete1: false,
        DeleteAll: false,
        Sum : false,
        Thx : false,
    }
},
methods: {
    getCartData() {
        let rawData = JSON.parse(localStorage.getItem("products"));
        if (rawData) {
            this.cartData = rawData;
            console.log(this.cartData)
        } else {
            this.cartData = [];
            console.log(this.cartData)
        }
        this.setTotal();
    },
    deleteAll() {
        this.cartData = [];
        localStorage.removeItem("products");
        this.DeleteAll = false;
        this.getCartData();
    },
    delete1(id) {
        for (let i = 0; i < this.cartData.length; i++) {
            if (this.cartData[i].id === id) {
                this.cartData.splice(i, 1);
                localStorage.setItem("products", JSON.stringify(this.cartData));
                this.DeleteAll = false;
            }
        }
        this.getCartData();
    },
    accumulateQty(id, qty, stock) {
        //get data with the same id
        for (let i = 0; i < this.cartData.length; i++) {
            if (this.cartData[i].id === id) {
                if (qty == 1) {
                    if (this.cartData[i].qty < stock) {
                        this.cartData[i].qty += qty;
                    } else if (this.cartData[i].qty >= stock) {
                        this.cartData[i].qty = stock;
                    }
                } else if (qty == -1) {
                    if (this.cartData[i].qty < 1) {
                        this.cartData[i].qty = 1;
                    } else if (this.cartData[i].qty > 1) {
                        this.cartData[i].qty += qty;
                    }
                } else if (this.cartData[i].qty > stock) {
                    this.cartData[i].qty = stock;
                } else if (this.cartData[i].qty < 1) {
                    this.cartData[i].qty = 1;
                }
                this.cartData[i].subTotal = this.cartData[i].qty * this.cartData[i].netPrice
            }
        }
        localStorage.setItem("products", JSON.stringify(this.cartData));
        this.getCartData();
    },
    setTotal() {
        if (!this.cartData.length == 0) {
            //set to 0
            this.allPrice = 0;
            this.allQty = 0;
            for (let i = 0; i < this.cartData.length; i++) {
                //accumulate
                this.allPrice += this.cartData[i].price * this.cartData[i].qty;
                this.allQty += this.cartData[i].qty;
                console.log(this.allPrice);
            }
        } else {
            this.allPrice = 0;
            this.allQty = 0;
            console.log(this.allPrice);
            console.log(this.allQty);
        }
    },
},
mounted() {
    this.getCartData()
}
}
</script>