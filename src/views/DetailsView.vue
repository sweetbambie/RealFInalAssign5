<script setup>
import axios from "axios";
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

// Define refs to store the response data
const response = ref(null);

// Get the movie ID from the route params
const route = useRoute();

onMounted(async () => {
  try {
    // Fetch movie details by ID
    const res = await axios.get(`https://api.themoviedb.org/3/movie/${route.params.id}?api_key=${import.meta.env.VITE_TMDB_KEY}&append_to_response=videos`);
    response.value = res.data; // Store the response in the ref
  } catch (error) {
    console.error("Error fetching movie details:", error);
  }
});
</script>

<template>
  <div v-if="response" class="movie-detail">
    <h1 class="movie-title">{{ response.original_title }}</h1>
    <p class="movie-overview">{{ response.overview }}</p>
    <p class="movie-release-date">Release Date: {{ response.release_date }}</p>
    <a class="movie-site" :href="response.homepage" target="_blank">Official Movie Site</a>
    <img :src="`https://image.tmdb.org/t/p/w500${response.poster_path}`" alt="Movie Poster" class="movie-poster" />

    <h2 class="trailers-title">Trailers</h2>
    <div class="trailers-container">
      <div v-for="trailer in response.videos.results" :key="trailer.id" class="trailer-tile">
        <a :href="`https://www.youtube.com/watch?v=${trailer.key}`" target="_blank">
          <img :src="`https://img.youtube.com/vi/${trailer.key}/hqdefault.jpg`" alt="Trailer"
            class="trailer-thumbnail" />
        </a>
      </div>
    </div>
  </div>

  <!-- Loader or empty state if the data is not loaded yet -->
  <div v-else>
    <p>Loading movie details...</p>
  </div>
</template>

<style scoped>
.movie-detail {
  padding: 20px;
}

.movie-title {
  font-size: 2rem;
  font-weight: bold;
}

.movie-overview {
  font-size: 1.2rem;
  color: #555;
}

.movie-release-date {
  font-size: 1rem;
  color: #777;
}

.movie-site {
  display: inline-block;
  margin-top: 10px;
  font-size: 1.1rem;
  color: #007BFF;
}

.movie-poster {
  max-width: 100%;
  border-radius: 8px;
  margin-top: 20px;
}

.trailers-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-top: 30px;
}

.trailers-container {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}

.trailer-tile {
  width: 200px;
  text-align: center;
}

.trailer-thumbnail {
  max-width: 100%;
  border-radius: 8px;
}
</style>
