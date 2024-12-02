<template>
    <div>
      <h1>Featured Movies</h1>
      <div class="movie-grid">
        <div v-for="movie in selectedMovies" :key="movie.id" class="movie-card">
          <img :src="getImageUrl(movie.poster_path)" :alt="movie.title" width="200" />
          <h3>{{ movie.title }}</h3>
          <p>{{ movie.overview }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from "vue";
  
  export default {
    setup() {
      const selectedMovieIds = [
        210577,  
        253257,      
        123634,
        9464
      ];
  
      const selectedMovies = ref([]);
  
      const fetchMovieDetails = async (id) => {
        const url = `https://api.themoviedb.org/3/movie/${id}?api_key=b748e5e23f131d901f8ab54ef85b8483&language=en-US`;
  
        try {
        const response = await fetch(url);
        if (!response.ok) {
          console.error("Failed to fetch movie details");
          return null; 
        }
        const data = await response.json();
        return data;  
      } catch (error) {
        console.error("Error fetching movie details:", error);
        return null;  
      }
    };
  
      const fetchSelectedMovies = async () => {
        const movieDetailsPromises = selectedMovieIds.map((id) => fetchMovieDetails(id));
        const moviesData = await Promise.all(movieDetailsPromises);
        selectedMovies.value = moviesData.filter(movie => movie !== null); 
      };
  
      onMounted(fetchSelectedMovies);
  
      const getImageUrl = (path) => {
        return path ? `https://image.tmdb.org/t/p/w500${path}` : 'https://via.placeholder.com/200x300?text=No+Image';
      };
  
      return {
        selectedMovies,
        getImageUrl
      };
    }
  };
</script>
  
<style scoped>
  h1 {
    text-align: center;
  }
  
  .movie-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 4%;
  }
  
  .movie-card {
    width: 20%;
    text-align: center;
    border: 1px solid hotpink;
    border-radius: 8px;
    padding: 10px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .movie-card img {
    border-radius: 8px;
    max-width: 100%;
    height: auto;
  }
  
  h3 {
    font-size: 1.2rem;
    margin-top: 10px;
  }
  
  p {
    font-size: 1rem;
    margin-top: 10px;
    color: #c5a6a6;
  }
  </style>
  
  
  
