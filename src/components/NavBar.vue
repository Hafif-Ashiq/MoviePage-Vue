<template>
    <div
        class="flex flex-col md:flex-row justify-between items-center bg-bgPrimary text-white py-[16px] px-4 md:px-[48px] gap-4 md:gap-0">
        <div class="flex flex-col md:flex-row items-center gap-4 md:gap-16">
            <img src="../assets/vue.svg" alt="logo" class="w-10 h-10" />
            <div
                class="flex flex-wrap justify-center md:justify-between items-center gap-[16px] font-bold text-[16px] md:text-[18px]">
                <div v-for="link in NAV_LINKS">
                    <a :href="link.path">{{ link.name }}</a>
                </div>
            </div>
        </div>
        <div class="flex flex-wrap items-center justify-center gap-[16px] font-bold">
            <div class="text-white text-[14px] md:text-[16px]">Plus</div>
            <div class="border-2 border-white rounded-[2px]">
                <p class="text-[12px] md:text-[14px] p-[4px]">EN</p>
            </div>
            <button
                class="px-[12px] md:px-[16px] py-[6px] md:py-[8px] rounded-md text-[14px] md:text-[16px]">Login</button>
            <button class="px-[12px] md:px-[16px] py-[6px] md:py-[8px] rounded-md text-[14px] md:text-[16px]">Join
                TMDB</button>
            <button
                class="px-[12px] md:px-[16px] py-[6px] md:py-[8px] rounded-md text-[14px] md:text-[16px] text-secondary hover:underline">Search</button>
        </div>
    </div>
</template>

<script setup>
import { NAV_LINKS } from '../constants';
</script>
