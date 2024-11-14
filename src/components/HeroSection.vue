<template>
    <div
        class="flex flex-col md:flex-row items-start justify-center bg-bgPrimary py-[24px] md:py-[48px] px-4 md:px-32 gap-[24px] md:gap-[48px] transition-all duration-300">
        <div class="w-full md:basis-[40%] flex justify-center md:justify-end items-center">
            <button @click="isModalOpen = true" class="w-[280px] md:w-[350px] relative group">
                <img :src="props.movieData.Poster" alt="movieTitle" class="w-full h-full object-cover rounded-[10px]">
                <div
                    class="absolute top-0 left-0 w-full h-full bg-black opacity-50 rounded-[10px] hidden group-hover:flex text-white text-[20px] md:text-[24px] font-semibold items-center justify-center">
                    Expand
                </div>
            </button>

            <!-- Image Modal -->
            <div v-if="isModalOpen" class="fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50">
                <div class="relative max-w-[90vw] max-h-[90vh]">
                    <img :src="props.movieData.Poster" alt="movieTitle" class="max-w-full h-[90vh] object-contain">
                    <button @click="isModalOpen = false"
                        class="absolute top-4 right-4 text-white text-2xl">&times;</button>
                </div>
            </div>
        </div>
        <div class="w-full md:basis-[60%] h-full text-white flex flex-col gap-[16px] md:gap-[24px] px-4 md:px-0">
            <!-- Title -->
            <div class="text-[32px] md:text-[48px] font-semibold">{{ props.movieData.Title }}</div>
            <!-- Release date, _ genre and total time of movie -->
            <div class="text-[16px] md:text-[18px] flex flex-col  flex-wrap gap-4">
                <div>
                    <!-- <span class="font-semibold">Rating:</span> -->
                    <span class="text-gray-500 px-2 border-gray-500 border-2 border-solid ml-2">{{ props.movieData.Rated
                        }}</span>
                </div>
                <div>
                    <span class="font-semibold">Release Date:</span>
                    <span class="ml-2">{{ props.movieData.Released }}</span>
                </div>
                <div>
                    <span class="font-semibold">Genre:</span>
                    <span class="ml-2">{{ props.movieData.Genre }}</span>
                </div>
                <div>
                    <span class="font-semibold">Duration:</span>
                    <span class="ml-2">{{ props.movieData.Runtime }}</span>
                </div>
            </div>
            <!-- User Score -->
            <div class="text-[16px] md:text-[18px] flex flex-wrap items-center gap-4">
                <div class="flex items-center gap-2">
                    <div class="relative w-10 h-10 md:w-12 md:h-12">
                        <!-- Background circle with 50% opacity -->
                        <div class="absolute w-full h-full rounded-full border-4 border-green-500/50"></div>
                        <!-- Rating text -->
                        <div
                            class="absolute inset-0 flex items-center justify-center font-semibold text-[14px] md:text-[16px]">
                            {{ props.movieData.Ratings[2].Value.split('/')[0] }}
                        </div>
                    </div>
                </div>
                <div class="flex items-center gap-2 justify-center flex-wrap">
                    <div class="text-[20px] md:text-[24px] font-semibold">{{ props.movieData.imdbRating }}</div>
                    <div class="text-[16px] md:text-[18px]">● {{ props.movieData.imdbVotes }} votes</div>
                </div>
            </div>
            <!-- like, share options -->
            <div class="flex items-center gap-4">
                <button class="text-[16px] md:text-[18px]">Like</button>
                <button class="text-[16px] md:text-[18px]">Share</button>
            </div>
            <!-- Overview -->
            <div class="flex flex-col gap-3 md:gap-4">
                <div class="font-semibold text-[20px] md:text-[24px]">Overview</div>
                <div class="text-[16px] md:text-[18px] max-w-full md:max-w-[700px]">
                    {{ props.movieData.Plot }}
                </div>
            </div>
            <!-- Cast -->
            <div class="flex flex-col gap-3 md:gap-4">
                <div class="font-semibold text-[20px] md:text-[24px]">Cast</div>
                <div class="text-[16px] md:text-[18px] grid grid-cols-2  md:grid-cols-3 gap-4">
                    <div class="flex flex-col items-start gap-1" v-for="castMember in cast">
                        <div class="text-[16px] md:text-[18px] font-semibold">{{ castMember.name }}</div>
                        <div class="text-[14px] md:text-[16px]">{{ castMember.role }}</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { onMounted, ref } from 'vue';
const props = defineProps(['movieData']);

const cast = ref([]);

onMounted(() => {
    cast.value.push({
        name: props.movieData.Director,
        role: "Director"
    });
    for (let i = 0; i < props.movieData.Writer.split(',').length; i++) {
        const existingMember = cast.value.find(member => member.name.trim() === props.movieData.Writer.split(',')[i].trim());
        if (existingMember) {
            existingMember.role += ", Writer";
            continue;
        }
        cast.value.push({
            name: props.movieData.Writer.split(',')[i],
            role: "Writer"
        });
    }
    for (let i = 0; i < props.movieData.Actors.split(',').length; i++) {
        cast.value.push({
            name: props.movieData.Actors.split(',')[i],
            role: "Actor"
        });
    }
})

const isModalOpen = ref(false);


</script>