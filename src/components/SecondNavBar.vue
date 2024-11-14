<template>
    <div class="flex justify-center items-center ">
        <div v-for="link in SECOND_NAV_LINKS">
            <div class="relative group">
                <button class="px-4 py-2 hover:text-secondary text-[18px] font-semibold">
                    {{ link.name }}
                </button>
                <div class="absolute left-0 hidden group-hover:block hover:block bg-white shadow-lg rounded-md mt-0">
                    <div v-for="option in link.options"
                        class="px-4 py-2 hover:bg-gray-100 text-gray-700 whitespace-nowrap cursor-pointer">
                        {{ option }}
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script setup>
import { SECOND_NAV_LINKS } from '../constants';
</script>
