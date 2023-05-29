<template>
    <section class="mx-7">
            <h2 class="font-bold text-4xl my-6">Exploler Airbnb</h2>
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-4 gap-y-8">
                <div class="bg-white shadow-lg rounded" v-for="item in airbnb.explore" :key="item.id">
                    <div class="flex flex-col rounded-lg bg-white  md:max-w-xl md:flex-row">
                        <img
                        class="h-96 w-full rounded-t-lg object-cover md:h-auto md:w-48 md:rounded-none md:rounded-l-lg"
                        :src="item.image"
                        alt="" />
                        <div class="flex flex-col justify-start p-6">
                            <h5 class="mb-2 text-xl font-medium">
                                {{ item.name }}
                            </h5>
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