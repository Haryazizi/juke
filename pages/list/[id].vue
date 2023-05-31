<script setup>
const {id} = useRoute().params;
const { data: airbnb } = useFetch('https://dummyjson.com/products/' + id)
</script>

<template>
    <section class="mx-20">
        <div>
            <NuxtLink to="/">
                <button class="bg-blue-500 hover:bg-blue-700 text-white text-xs font-bold py-2 px-4 mb-[80px]">
                Kembali
                </button>
            </NuxtLink>
            <div class="det-img grid grid-cols-3 gap-[1px] w-full h-full rounded-[10px]">
                <div v-for="(image, index) in airbnb.images" :key="index" class="">
                    <img :src="image" class="object-cover object-top hover:scale-110 flex">
                </div>
                <div>
                    <div>
                        <h2 class="text-5xl text-start text-[#484848] font-bold mt-9">{{ airbnb.title }}</h2>                                       
                    </div>
                    <div>
                        <h4 class="text-xl text-start text-[#767676] font-bold uppercase mt-[8px]">{{ airbnb.description }}</h4>
                    </div>
                    <p class="text-4xl text-start text-[#484848] font-bold">Price : ${{ airbnb.price }}</p>
                    <div class="flex gap-1 w-full font-bold mt-[8px]">
                        <p class="text-4xl text-start text-[#484848]"> Rating : {{ airbnb.rating }}</p>
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="gold" class="w-[36px] h-[36px] mt-1">
                        <path fill-rule="evenodd" d="M10.788 3.21c.448-1.077 1.976-1.077 2.424 0l2.082 5.007 5.404.433c1.164.093 1.636 1.545.749 2.305l-4.117 3.527 1.257 5.273c.271 1.136-.964 2.033-1.96 1.425L12 18.354 7.373 21.18c-.996.608-2.231-.29-1.96-1.425l1.257-5.273-4.117-3.527c-.887-.76-.415-2.212.749-2.305l5.404-.433 2.082-5.006z" clip-rule="evenodd" />
                        </svg>
                    </div>
                    <div>
                        <p class="text-4xl text-start text-[#484848] font-bold">Stock : {{ airbnb.stock }}</p>
                        <p class="text-4xl text-start text-[#484848] font-bold">Brand : {{ airbnb.brand }}</p>
                        <p class="text-4xl text-start text-[#484848] font-bold">Category : {{ airbnb.category }}</p>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>