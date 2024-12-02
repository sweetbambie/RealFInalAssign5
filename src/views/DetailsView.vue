<script setup>
import axios from "axios";
import { useRoute } from "vue-router";

const route = useRoute();
const response = await axios.get(`https://api.themoviedb.org/3/movie/${route.params.id}?api_key=${import.meta.env.VITE_TMDB_KEY}&append_to_response=videos`);
console.log(response.data);
</script>

<template>
  <div class="movie-detail">
    <h1 class="movie-title">{{ response.data.original_title }}</h1>
    <p class="movie-overview">{{ response.data.overview }}</p>
    <p class="movie-release-date">Release Date: {{ response.data.release_date }}</p>
    <a class="movie-site" :href="response.data.homepage" target="_blank">Official Movie Site</a>
    <img :src="`https://image.tmdb.org/t/p/w500${response.data.poster_path}`" alt="Movie Poster" class="movie-poster" />

    <h2 class="trailers-title">Trailers</h2>
    <div class="trailers-container">
      <div v-for="trailer in response.data.videos.results" :key="trailer.id" class="trailer-tile">
        <a :href="`https://www.youtube.com/watch?v=${trailer.key}`" target="_blank">
          <img :src="`https://img.youtube.com/vi/${trailer.key}/hqdefault.jpg`" alt="Trailer"
            class="trailer-thumbnail" />
        </a>
      </div>
    </div>
  </div>
</template>

<style scoped>
.movie-detail {
  text-align: center;
  margin: 20px;
}

.movie-title {
  font-size: 2rem;
  font-weight: bold;
}

.movie-overview {
  font-size: 1.1rem;
  margin-top: 10px;
}

.movie-release-date {
  font-size: 1.1rem;
  margin-top: 10px;
}

.movie-site {
  margin-top: 10px;
  font-size: 1.1rem;
}

.movie-poster {
  width: 300px;
  margin-top: 20px;
}

.trailers-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.trailer-tile {
  margin: 10px;
}

.trailer-thumbnail {
  width: 200px;
  height: 113px;
}

.trailers-title {
  margin-top: 30px;
  font-size: 1.5rem;
  font-weight: bold;
}
</style>

  
