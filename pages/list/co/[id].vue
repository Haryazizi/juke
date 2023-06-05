<template>
    <section class="mx-20">
        <div class="pt-24">
            <NuxtLink onclick="window.history.go(-1); return false;">
                <button class="bg-red-500 hover:bg-red-700 text-white text-xs font-bold py-2 px-4 mb-[80px]">
                Kembali
                </button>
            </NuxtLink>
        </div>
        <div class="flex flex-col justify-center items-center px-7 py-4">
            <form class="bg-white shadow-lg rounded px-8 pt-6 pb-8 mb-4 flex">
                <div class="grid lg:grid-cols-3 sm:grid-cols-1">
                    <div class="w-[188px]">
                        <div>
                            <div>
                                <img :src="airbnb.thumbnail" alt="" class="w-[188px] h-[240px] object-cover object-top">
                            </div>
                            <div>
                                <div>
                                    <h2 class="text-[16px] text-start text-[#484848] font-bold mt-1">{{ airbnb.title }}</h2>                                       
                                </div>
                                <div>
                                    <h4 class="text-[10px] text-start text-[#767676] font-bold uppercase mt-[8px]">{{ airbnb.description }}</h4>
                                </div>
                                <p class="text-[14px] text-start text-[#484848] font-bold">${{ airbnb.price }}</p>
                                <div class="flex gap-1 w-full font-bold mt-[8px]">
                                    <p class="text-[12px] text-start text-[#008489]">{{ airbnb.rating }}</p>
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="#008489" class="w-[8px] h-[8px] mt-1.5">
                                    <path fill-rule="evenodd" d="M10.788 3.21c.448-1.077 1.976-1.077 2.424 0l2.082 5.007 5.404.433c1.164.093 1.636 1.545.749 2.305l-4.117 3.527 1.257 5.273c.271 1.136-.964 2.033-1.96 1.425L12 18.354 7.373 21.18c-.996.608-2.231-.29-1.96-1.425l1.257-5.273-4.117-3.527c-.887-.76-.415-2.212.749-2.305l5.404-.433 2.082-5.006z" clip-rule="evenodd" />
                                    </svg>
                                </div>
                            </div>
                        </div> 
                    </div>
                    <div class="mb-4">
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
                            Jumlah Barang
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="jml" type="number" min="1" placeholder="Jumlah" value="1" @change="total();" @keyup="total();"/>
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
                        <textarea class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Alamat" cols="35" rows="6"></textarea>
                    </div>
                    <div class="mt-4 ml-4">
                        <p class="text-4xl text-[#484848] border border-black px-2 py-2 font-bold">Stock :<input class="w-[50px] ml-1" id="stk" type="text" :value="airbnb.stock" disabled></p>
                        <label class="block text-gray-700 text-sm font-bold mb-2 mt-2">
                        Total Harga
                        </label>
                        <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="ttl" name="ttl" type="text" :value="airbnb.price" disabled>
                        <div class="flex items-center justify-end mt-4">
                            <input  id="hrg" type="hidden" :value="airbnb.price"/>
                            <button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button" @click="krg();">
                                Beli
                            </button>
                        </div>
                    </div>
                </div>
            </form>    
        </div>
    </section>   
</template>

<script setup>
const {id} = useRoute().params;
const { data: airbnb } = await useFetch('https://dummyjson.com/products/' + id)


</script>

<script>
function total() {
    var grand_total = document.getElementById('jml').value * document.getElementById('hrg').value;
    if (!isNaN(grand_total)) {
        document.getElementById('ttl').value = grand_total;        
    }
}

function krg() {
    var stk = document.getElementById('stk').value - document.getElementById('jml').value;
    if (!isNaN(stk)) {
        document.getElementById('stk').value = stk;        
    }
}
</script>
