<template>
    <section class="mx-20">
        <div>
            <h2 class="font-bold text-4xl my-16">Expériences très bien notées</h2>
            <p class="font-light my-5">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et logements compris</p>
            <div class="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-6 gap-3 gap-y-8">
                <div class="bg-white shadow-lg w-[188px] h-full hover:scale-110 hover:shadow-lg" v-for="item in airbnb.expe" :key="item.id">
                        <div>
                            <div>
                                <img :src="item.image" alt="" class="relative overflow-hidden rounded-lg bg-cover bg-no-repeat text-center">
                            </div>
                            <div class="p-4">
                                <div>
                                    <h4 class="text-[10px] text-start text-[#767676] font-bold uppercase mt-[8px]">{{ item.description }}</h4>
                                </div>
                                <div>
                                    <h2 class="text-[16px] text-start text-[#484848] font-bold mt-1">{{ item.name }}</h2>
                                </div>
                                <p class="text-[14px] text-start text-[#484848] font-light">{{ item.price }}</p>
                                <div class="flex gap-1 w-full font-bold mt-[8px]">
                                    <p class="text-[12px] text-start text-[#008489]">{{ item.rating }}</p>
                                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="blue" class="w-5 h-5">
                                    <path fill-rule="evenodd" d="M10.788 3.21c.448-1.077 1.976-1.077 2.424 0l2.082 5.007 5.404.433c1.164.093 1.636 1.545.749 2.305l-4.117 3.527 1.257 5.273c.271 1.136-.964 2.033-1.96 1.425L12 18.354 7.373 21.18c-.996.608-2.231-.29-1.96-1.425l1.257-5.273-4.117-3.527c-.887-.76-.415-2.212.749-2.305l5.404-.433 2.082-5.006z" clip-rule="evenodd" />
                                    </svg>
                                </div>
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