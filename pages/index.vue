<template>
  <div class="home">
    <!-- Hero -->
    <Hero />

    <!-- Movies -->
    <div class="movies container">
      <div id="movie-grid" class="movie-grid">
        <div class="movie" v-for="(movie, index) in movies" :key="index">
          <div class="movie-img">
            <img :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`" alt="">
            <p class="review">{{ movie.vote_average }}</p>
            <p class="review">{{ movie.overview }}</p>
          </div>
          <div class="info">
            <p class="title">{{ movie.title.slice(0, 25) }}
              <span v-if="movie.title.length > 25">...</span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        movies: [],
      }
    },
    async fetch() {
      await this.getMovies();
    },
    methods: {
      async getMovies() {
        const data = axios.get(
          "https://api.themoviedb.org/3/movie/now_playing?api_key=4da10dd7595edfe861411e559dde71dc&language=en-US&page=1"
        );

        const result = await data;
        result.data.results.forEach(movie => {
          this.movies.push(movie)
        });
        console.log(this.movies);
      }
    }
  }
</script>
