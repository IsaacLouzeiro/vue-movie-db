<template>
    <header>
        <div class="bg-header"></div>
        <div class="content-header">
            <div>
                <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
                <div class="movie-detail">
                    <p><span>Released date: </span> {{ movie.Released }}</p>
                    <p><span>Genre: </span> {{ movie.Genre }}</p>
                    <p><span>Director: </span> {{ movie.Director }}</p>
                    <p><span>Writer: </span> {{ movie.Writer }}</p>
                    <p><span>Actors: </span> {{ movie.Actors }}</p>
                    <p><span>Country: </span> {{ movie.Country }}</p>
                </div>
            </div>
            
            <div>
                <h1>{{ movie.Title }}</h1>
                <p class="type-movie">{{ movie.Type }}</p>
                <p class="plot-movie">{{ movie.Plot }}</p>
            </div>
        </div>
    </header>

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
      fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`).then(response => response.json()).then(data => {
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
//colors
    $color1: #357ded;
    $color2: #151515;
    $color3: #32e875;
    $color4: #e1e5ee;
    $color5: #5438dc;

    header {
            background-color: $color2;
            position: relative;
            height: 300px;
            display: flex;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;

            .bg-header {
                background-image: url('~@/assets/bg-header.jpg');
                filter: blur(2px);
                background-size: 100%;
                background-position: center;
                opacity: .6;
                width: 100%;
                height: 100%;
                position: absolute;

            }

            .content-header {
                position: relative;
                z-index: 1;
                width: 100%;
                max-width: 1400px;
                padding: 0 20px;
                padding-top: 100px;
                display: flex;
                flex-wrap: wrap;

                h1 {
                    color: $color4;
                    font-size: 3.4em;
                    margin-bottom: 15px;
                    text-shadow: 1px 1px 10px rgba(0, 0, 0, .8);
                }

                .type-movie {
                    background-color: $color5;
                    margin: 10px 0;
                    width: 80px;
                    height: 45px;
                    color: $color4;
                    font-size: 1.2em;
                    display: flex;
                    justify-content: center;
                    align-items: center;
                }

                .plot-movie {
                    display: inline-block;
                    width: 100%;
                    max-width: 500px;
                    margin-left: auto;
                    margin-top: 100px;
                }

                .movie-detail {
                    padding: 5px 0;
                    
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
                        color: $color2;
                        font-size: 1em;
                        line-height: 1.4;
                        margin: 3px 0;

                        span {
                            color: $color5;
                        }
                    }
                }
            }
        }


</style>