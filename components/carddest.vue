<template>
    <section class="mx-20">
        <div class="flex flex-col gap-5 text-slate-700 mt-20 mb-40">
            <div>
                <h1 class="text-xl font-bold">Destinations Airbnb Plus à la Une</h1>
                <p class="font-light">Voyages de plusieurs jours organisés par des experts locaux avec activités, repas et
                    logements compris</p>
            </div>
            <div class="grid lg:grid-cols-3 sm:grid-cols-2 gap-5 w-full">
                <div class="flex flex-col gap-3 rounded hover:cursor-pointer"  v-for="item in airbnb.dest" :key="item.id">
                    <div class="flex justify-center items-center h-64 bg-[url('/img/ds2.png')] bg-no-repeat bg-cover bg-center hover:saturate-150 rounded ">
                        <span><img src="/img/logo.png" alt=""></span>
                    </div>
                    <h3 class="text-[14px] mt-1 font-bold text-fuchsia-900">
                        {{ item.name }}
                    </h3>
                    <p>{{ item.price }}</p>
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