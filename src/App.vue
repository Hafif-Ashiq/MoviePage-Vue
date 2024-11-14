<script setup>
import NavBar from './components/NavBar.vue'
import SecondNavBar from './components/SecondNavBar.vue'
import { onMounted, ref } from 'vue';
import HeroSection from './components/HeroSection.vue'

const movieData = ref(null);

onMounted(() => {
  const getMovieData = async () => {
    const response = await fetch('http://www.omdbapi.com/?i=tt3896198&apikey=d2132124');
    const data = await response.json();
    movieData.value = data;
  };
  getMovieData();
});

</script>

<template>
  <div>
    <NavBar />
    <SecondNavBar />
    <HeroSection :movieData="movieData" />
  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}

.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
