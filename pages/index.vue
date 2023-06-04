<template> 
    <div>
      <main class="">
        <section class="min-h-screen flex items-center bg-[url(/img/bg.png)] md:bg-fixed bg-cover">
          <div class="max-w-sm rounded overflow-hidden shadow-lg ml-20 bg-white">
            <div class="px-6 py-4">
              <div class="font-bold text-xl mb-2">Réservez des hébergements et des activités uniques.</div>
                <form class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
                  <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">
                      Où
                    </label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="Partout">
                  </div>
                  <div class="mb-4 flex">
                    <label class="block text-gray-700 text-sm font-bold mb-2">
                      Arrivée
                    </label>      
                    <label class="block text-gray-700 text-sm font-bold ml-20">
                      Départ
                    </label>
                  </div>
                  <div class="mb-4 flex justify-center">
                    <input class="shadow rounded w-full py-2 px-3" id="date" type="date">
                    <input class="shadow rounded w-full py-2 px-3" id="date" type="date">
                  </div>
                  <div class="mb-4">
                    <label class="block text-gray-700 text-sm font-bold mb-2">
                      Voyageurs
                    </label>
                    <input class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="TVoyageurs">
                  </div>
                  <div class="flex items-center justify-end">
                    <button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" type="button">
                      Rechercher
                    </button>
                  </div>
              </form>
            </div>
          </div>
        </section>
        
        
        <div class="pt-12 flex items-center justify-center">
          <NuxtLink to="list">
            <button class="bg-red-500 hover:bg-red-500 text-white font-bold py-2 px-9 rounded focus:outline-none focus:shadow-outline" type="button">
              List Product
            </button>
          </NuxtLink>
        </div>

        <Cardex />
        <Hebergements />
        <Cardaven />
        <Cardlogem />
        <Cardexpe />
        <Carddest />        
      </main>   
    </div>
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