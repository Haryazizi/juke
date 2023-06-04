<script setup>
const { data: airbnb } = await useFetch('https://dummyjson.com/products/categories')
</script>
<template>
    <div>
    <div>
        <p class="pt-12 pb-5 flex justify-center text-4xl font-bold">Product Categories</p>
    </div>
    
    <Search />
    
    <div class="flex">
        <div class="grid grid-cols-2 w-[500px] h-[200px] lg:pl-8 lg:place-content-center md:w-[740px] lg:w-full overflow-y-auto lg:h-[300px] lg:overflow-y-hidden lg:grid-cols-4 xl:grid-cols-5 md:grid-cols-3 gap-2 py-5 rounded-xl">
            <NuxtLink :to="'/list/categories/' + category"
                class="border bg-white h-10 flex items-center min-w-[175px] rounded-xl hover:shadow hover:cursor-pointer hover:scale-110  active:bg-black"
                v-for="category in airbnb">
                        <div class="flex mx-6 overflow-x-auto">
                            {{ category.toUpperCase().split('-').join(' ') }}
                        </div>
            </NuxtLink>
        </div>
    </div>
    </div>
</template>