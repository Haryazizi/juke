<template>
    <section class="mx-20">
        <div>
        <h2 class="font-bold text-4xl my-6">Logements dans le monde entier</h2>
            <div class="grid grid-cols-2 sm:grid-cols-2 lg:grid-cols-4 gap-3 gap-y-8">
                <div class="bg-white shadow-lg w-[290px] h-full hover:scale-110 hover:shadow-lg" v-for="item in airbnb.logem" :key="item.id">
                        <div>
                            <div>
                                <img :src="item.image" alt="" class="w-[290px] h-[265px] object-cover object-top">
                            </div>
                            <div class="p-4">
                                <div class="flex justify-start">
                                    <button type="button" class="bg-transparent rounded border-2 border-black px-[8px] py-[8px] text-xs font-medium uppercase leading-normal text-black flex justify-start">
                                    Superhost
                                    </button>
                                    <h4 class="text-[12px] text-[#767676] font-normal">{{ item.description }}</h4>
                                    <div class="ml-[80px] flex gap-2 w-full font-bold">
                                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="red" class="w-5 h-5">
                                        <path fill-rule="evenodd" d="M10.788 3.21c.448-1.077 1.976-1.077 2.424 0l2.082 5.007 5.404.433c1.164.093 1.636 1.545.749 2.305l-4.117 3.527 1.257 5.273c.271 1.136-.964 2.033-1.96 1.425L12 18.354 7.373 21.18c-.996.608-2.231-.29-1.96-1.425l1.257-5.273-4.117-3.527c-.887-.76-.415-2.212.749-2.305l5.404-.433 2.082-5.006z" clip-rule="evenodd" />
                                        </svg>
                                        <p class="text-[12px] text-[#484848] font-medium">{{ item.rating }}</p>
                                    </div>
                                </div>
                                <p class="text-start text-[14px] text-[#484848] font-normal mt-2">{{ item.price }}</p>
                            </div>
                        </div>
                </div>
            </div>
        </div> 
    </section> 
</template>
<script>
import json from '@/assets/data/airbnb.json';
export default {
    data() {
        return {
            layouts: {
                header: "header",
                footer: "footer"
            },
            airbnb: json,
        }
    },
}
</script>