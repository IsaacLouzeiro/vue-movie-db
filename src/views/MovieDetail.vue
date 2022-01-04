<template>
  <div class="movie-detail">
    <h2>{{ movie.Title }}</h2>
    <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
    <p><span>Runtime</span> {{ movie.Runtime }}</p>
    <p><span>Country</span> {{ movie.Country }}</p>
    <p><span>By</span> {{ movie.Writer }}</p>
    <p><span>Genre</span> {{ movie.Genre }}</p>
    <p><span>Year</span> {{ movie.Year }}</p>
    <p class="type-movie">{{ movie.Type }}</p>
    <p class="plot-movie">{{ movie.Plot }}</p>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from 'vue-router';
import env from '@/env.js';

export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`).then(response => response.json()).then(data => {
        movie.value = data;
        console.log(data)
      })
    });

    return {
      movie
    }
  }
}
</script>

<style lang="scss" scoped>
.movie-detail {
  padding: 16px;
  
  h2 {
    color: #fff;
    font-size: 1.5em;
    font-weight: 600;
    margin-bottom: 16px;
  }

  .featured-img {
    display: block;
    max-width: 200px;
    margin-bottom: 10px;
  }
  
  p {
    color: #fff;
    font-size: 1em;
    line-height: 1.4;
    margin: 3px 0;

    span {
      color: #42b883;
    }
  }

  .plot-movie {
  }

  .type-movie {
    display: inline-block;
    padding: 5px 16px;
    background-color: #42b883;
    margin: 10px 0;
  }
}
</style>