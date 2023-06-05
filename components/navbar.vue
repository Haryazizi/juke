<template>
    <nav class="parallax fixed flex flex-row justify-between items-center w-full px-6 py-4 z-10 text-black">
        <NuxtLink to="/">
            <img class="w-[28.65px] h-[30.73px]" :src="navBrandSrc" alt="nav-brand">
        </NuxtLink>
        <div class="hidden md:flex item-center space-x-6">
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">Français (FR)</NuxtLink>
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">EUR €</NuxtLink>
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">Devenir hôte</NuxtLink>
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">Créer son expérience</NuxtLink>
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">Aide</NuxtLink>
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">Inscription</NuxtLink>
            <NuxtLink to="/" class="hover:text-[#FF5A5F]">Connexion</NuxtLink>
        </div>
        <div class="md:hidden">
            <button @click="toggleMobileMenu" class="block focus:outline-none">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
                </svg>
            </button>
            <div v-if="isMobileMenuOpen" class="absolute mt-[18px] left-0 w-full bg-white text-[#484848] border-t shadow">
                <div class="flex flex-col space-y-4 p-4">
                    <NuxtLink to="/">Français (FR)</NuxtLink>
                    <NuxtLink to="/">EUR €</NuxtLink>
                    <NuxtLink to="/">Devenir hôte</NuxtLink>
                    <NuxtLink to="/">Créer son expérience</NuxtLink>
                    <NuxtLink to="/">Aide</NuxtLink>
                    <NuxtLink to="/">Inscription</NuxtLink>
                    <NuxtLink to="/">Connexion</NuxtLink>
                </div>
            </div>
        </div>
        <div class="flex flex-col">
            <button @click="dropdownOpen = !dropdownOpen"
                class="flex flex-row items-center filter min-w-fit h-6 py-5 px-2 border border-gray-300 rounded-full font-normal shadow-sm hover:shadow-lg z-[2]">
                <img src="/img/menu.svg" alt="" class="h-5 mx-1">
                <img src="/img/user.svg" alt="" class="h-7 mx-1">
            </button>
            <div class="absolute w-screen h-screen top-0 right-0 bottom-0" 
            v-show="dropdownOpen"
            >
                <div class="absolute w-screen h-screen z-[1]" @click="dropdownOpen = !dropdownOpen"></div>
                <ul id="ddMenu"
                    class="absolute z-[2] w-[230px] font-normal text-slate-600 top-[64px] sm:right-10 right-0 bg-white p-5 visible rounded-lg">
                    <li class="mb-5 hover:text-slate-800 "><NuxtLink to="/login">Login</NuxtLink></li>
                    <li class="pt-5 hover:text-slate-800 border-t"><NuxtLink to="/list/cart"><span><img src="/img/cart.svg" alt="" class="h-4 inline mb-1 mr-2"></span>Keranjang Saya</NuxtLink></li>
                </ul>
            </div>
        </div>                        
    </nav>
</template>

<script setup>
    import {ref, onMounted, onBeforeUnmount} from 'vue';

    const nav = ref(null);
    const navBrandSrc = ref('/img/logo.png');
    const isMobileMenuOpen = ref(false);

    const onScroll = () => {
        if (document.documentElement.scrollTop > 60 || document.body.scrollTop > 60) {
            nav.value.classList.add('bg-white', 'items-center', 'shadow');
            nav.value.classList.remove('text-white');
            navBrandSrc.value = '/img/logo-red.png';
        } else {
            nav.value.classList.remove('bg-white', 'items-center', 'shadow');
            nav.value.classList.add('text-black');
            navBrandSrc.value = '/img/logo.png';
        }
    };

    const toggleMobileMenu = () => {
        isMobileMenuOpen.value = !isMobileMenuOpen.value;
    };

    onMounted(() => {
        nav.value = document.querySelector('nav');
        window.addEventListener('scroll', onScroll);
    });

    onBeforeUnmount(() => {
        window.removeEventListener('scroll', onScroll);
    });
</script>
<script>
export default {
    data() {
        return {
            dropdownOpen: false
        }
    },
}</script>