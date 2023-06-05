<template>
    <section class="mx-20">
        <div class="pt-6">
            <div class="pt-12 pb-4">
                <NuxtLink onclick="window.history.go(-1); return false;">
                    <button class="bg-red-500 hover:bg-red-500 text-white font-bold py-2 px-9 rounded focus:outline-none focus:shadow-outline" type="button">
                    Kembali
                    </button>
                </NuxtLink>
            </div>
            <div class="flex justify-center gap-2 items-center w-full h-[280px] mt-4 duration-1000">
                    
                <div class="flex flex-nowrap justify-center gap-2 h-full max-h-[235px] w-full">
                <div v-for="(image, index) in airbnb.images" :key="index" class="gw-[250px] h-[250px] object-cover aspect-square duration-1000 rounded-lg">
                    <img :src="image" class="object-cover object-top hover:scale-110 flex duration-1000">
                </div>
                </div>
            </div>                                
        </div>
    </section>
    <section class="mx-20 flex flex-col">
        <div class="mx-auto">
            <div class="p-5 rounded-lg border-[1px] border-black/[0.1] shadow-md flex-col gap-1 sticky top-right-0 md:flex hidden">
                <div>
                    <h2 class="text-4xl text-start text-[#484848] font-bold">{{ airbnb.title }}</h2>                                       
                </div>
                <div>
                    <h4 class="text-xl text-start text-[#767676] font-bold uppercase mt-[6px]">{{ airbnb.description }}</h4>
                </div>
                <p class="text-3xl text-start text-[#484848] font-bold">Price : ${{ airbnb.price }}</p>
                <div class="flex gap-2 w-full font-bold mt-[8px]">
                    <p class="text-3xl text-start text-[#484848]"> Rating : {{ airbnb.rating }}</p>
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="gold" class="w-[36px] h-[36px] mt-1">
                    <path fill-rule="evenodd" d="M10.788 3.21c.448-1.077 1.976-1.077 2.424 0l2.082 5.007 5.404.433c1.164.093 1.636 1.545.749 2.305l-4.117 3.527 1.257 5.273c.271 1.136-.964 2.033-1.96 1.425L12 18.354 7.373 21.18c-.996.608-2.231-.29-1.96-1.425l1.257-5.273-4.117-3.527c-.887-.76-.415-2.212.749-2.305l5.404-.433 2.082-5.006z" clip-rule="evenodd" />
                    </svg>
                </div>
                <div>
                    <p class="text-3xl text-start text-[#484848] font-bold mt-1">Stock : {{ airbnb.stock }}</p>
                    <p class="text-3xl text-start text-[#484848] font-bold mt-2">Brand : {{ airbnb.brand }}</p>
                    <p class="text-3xl text-start text-[#484848] font-bold mt-2">Category : {{ airbnb.category }}</p>
                </div>
                <div class="flex flex-col gap-4">
                    <NuxtLink :to="'co/' + airbnb.id">
                        <button class="bg-rose-500 w-full p-3 rounded-md text-white text-center text-[15px] font-bold">
                        Beli
                        </button>
                    </NuxtLink>
                    <button class="bg-rose-500 w-full p-3 rounded-md text-white text-center text-[15px] font-bold" @click="addToCart(id, stockCounter), toggleAddcartStatus = true">
                        <div class="flex justify-center">
                            + Keranjang
                            <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6 mt-1 ml-1">
                            <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
                            </svg>
                        </div>
                    </button>
                </div>
                <div class="flex flex-col justify-between w-[400px] h-20 rounded-lg p-4 bg-white z-20 shadow-lg mt-1" v-show="toggleAddcartStatus">
                    <div class="flex justify-start">
                        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="black" class="w-6 h-6 hover:cursor-pointer mt-1" @click="toggleAddcartStatus = false">
                        <path stroke-linecap="round" stroke-linejoin="round" d="M9.75 9.75l4.5 4.5m0-4.5l-4.5 4.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
                        </svg>
                        <div class="flex flex-col justify-center text-lg ml-2">
                            <div>
                                Berhasil Menambahkan Produk!
                            </div>
                            <div class="text-rose-500 hover:scale-105 active:scale-95 font-medium cursor-pointer items-center">
                                    <NuxtLink to="/list/cart">
                                        Lihat Keranjang Sekarang
                                    </NuxtLink>
                            </div>
                        </div>
                    </div>
                </div>
            </div>                       
        </div>                   
    </section>               
</template>

<script setup>
const {id} = useRoute().params;
const { data: airbnb } = useFetch('https://dummyjson.com/products/' + id)
</script>

<script>
export default {
    data() {
        return {
            stockCounter: 1,
            toggleAddcartStatus: false
        }
    },
    methods: {
        accumulateStock(n, stock) {
            if (n == 1) {
                if (this.stockCounter < stock) {
                    this.stockCounter += n;
                } else if (this.stockCounter >= stock) {
                    this.stockCounter = stock;
                }
            } else if (n == -1) {
                if (this.stockCounter < 1) {
                    this.stockCounter = 1;
                } else if (this.stockCounter > 1) {
                    this.stockCounter += n;
                }
            } else if (this.stockCounter > stock) {
                this.stockCounter = stock;
            } else if (this.stockCounter < 1) {
                this.stockCounter = 1;
            }
            console.log(this.stockCounter, stock);
        },
        async addToCart(id, qty) {
            let { data: product }  = await useFetch('https://dummyjson.com/products/' + id);
            let dataProduct        = product._rawValue;
            dataProduct.qty        = qty;
            dataProduct.noteStatus = false;
            //if localStorage products didn't exist
            if (!localStorage.getItem("products")) {
                let array = [];
                dataProduct.cartId = 1;
                dataProduct.subTotal = (this.price * this.stockCounter) + this.cleaningPrice + this.adminPrice;
                array.push(dataProduct);
                localStorage.setItem("products", JSON.stringify(array));
                console.log(JSON.parse(localStorage.getItem("products")));
            } 
            //if localStorage products is exist
            else {
                //get all data from localStorage
                let productAtCart = JSON.parse(localStorage.getItem("products"));
                let listProductId = [];
                //get ListProductId in localStorage
                for (let i = 0; i < productAtCart.length; i++) {
                    if (!listProductId.includes(productAtCart[i].id)) {
                        listProductId.push(productAtCart[i].id)
                    }
                }
                console.log(listProductId);
                
                //check if the id already exists or not
                if (!listProductId.includes(dataProduct.id)) {
                    //if not exist save to localStorage
                    dataProduct.cartId   = productAtCart.length + 1;
                    dataProduct.subTotal = (this.price * this.stockCounter) + this.cleaningPrice + this.adminPrice;
                    productAtCart.push(dataProduct);
                    localStorage.setItem("products", JSON.stringify(productAtCart));
                    console.log(JSON.parse(localStorage.getItem("products")));
                    console.log(listProductId);
                } else {
                    //if exist
                    //get data with the same id from localStorage
                    for (let j = 0; j < productAtCart.length; j++) {
                        //if data found
                        if (productAtCart[j].id === id) {
                            productAtCart[j].subTotal += (this.price * this.stockCounter) + this.cleaningPrice + this.adminPrice;
                            productAtCart[j].qty      += qty;
                            localStorage.setItem("products", JSON.stringify(productAtCart));
                            console.log(JSON.parse(localStorage.getItem("products")));
                        }
                    }
                }
                console.log(JSON.parse(localStorage.getItem("products")));
            }
        }
    },
    mounted() {
    }
}
</script>