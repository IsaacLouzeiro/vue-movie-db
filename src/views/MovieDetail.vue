<template>
    <header>
        <div class="bg-header"></div>
    </header>
    <section class="content-section">
        <div class="content-one">
            <h1 class="movieTitle-sm movieTitle">{{ movie.Title }}</h1>
            <img :src="movie.Poster" alt="Movie Poster" class="featured-img">
            <div class="resp">
                <h1 class="movieTitle-md movieTitle">{{ movie.Title }}</h1>
                <p class="type-movie type-movie-sm">{{ movie.Type }}</p>
                <div class="movie-detail">
                    <p><span>Released date: </span> {{ movie.Released }}</p>
                    <p><span>Genre: </span> {{ movie.Genre }}</p>
                    <p><span>Director: </span> {{ movie.Director }}</p>
                    <p><span>Writer: </span> {{ movie.Writer }}</p>
                    <p><span>Actors: </span> {{ movie.Actors }}</p>
                    <p><span>Country: </span> {{ movie.Country }}</p>
                </div>
            </div>
        </div>
        
        <div class="content-two">
            <h1 class="movieTitle-xl movieTitle">{{ movie.Title }}</h1>
            <p class="type-movie type-movie-xl">{{ movie.Type }}</p>
            <h3>Synopsis</h3>
            <p class="plot-movie">{{ movie.Plot }}</p>
        </div>
    </section>
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
    height: 250px;
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

    @media only screen and (max-width: 576px) {
        height: 200px;
    }
}

.movieTitle {
    color: $color4;
    font-size: 3.4em;
    margin-bottom: 15px;
    text-shadow: 1px 1px 10px rgba(0, 0, 0, .8);
}

.movieTitle-xl {
    font-size: 3.4em;
    display: inline-block;

    @media only screen and (max-width: 912px) {
        display: none;
    }
}

.movieTitle-md {
    display: none;

    @media only screen and (max-width: 912px) {
        font-size: 2em;
        display: inline-block;
    }

    @media only screen and (max-width: 576px) {
        display: none;
    }
}

.movieTitle-sm {
    display: none;

    @media only screen and (max-width: 576px) {
        font-size: 2em;
        display: block;
        width: 100%;
    }
}

.type-movie {
    background-color: $color5;
    margin: 10px 0;
    width: 80px;
    height: 40px;
    color: $color4;
    font-size: 1.2em;
    display: flex;
    justify-content: center;
    align-items: center;
}

.type-movie-xl {
    display: flex;

    @media only screen and (max-width: 912px) {
        display: none;
    }
}

.type-movie-sm {
    display: none;

    @media only screen and (max-width: 912px) {
        display: flex;
        width: 70px;
        height: 30px;
        font-size: 1em;
        color: $color4!important;
        margin-bottom: 15px!important;
    }
}

.content-section {
    position: relative;
    top: -150px;
    z-index: 1;
    width: 100%;
    max-width: 1400px;
    padding: 0 20px;
    margin: auto;
    display: flex;
    flex-wrap: nowrap;
    border: 1px solid;

    .content-one {

        @media only screen and (max-width: 576px) {
            display: flex;
            flex-wrap: wrap;
        }

        @media only screen and (max-width: 912px) {
            display: flex;
        }
    }

    .featured-img {
        display: block;
        margin-right: 20px;
        margin-bottom: 10px;
        
        @media only screen and (max-width: 912px) {
            max-width: 200px;
        }
    }

    h3 {
        color: $color5;
        margin-top: 50px;
        margin-bottom: 10px;
        @media only screen and (max-width: 912px) {
            margin-top: 15px;
        }
    }

    .plot-movie {
        display: inline-block;
        width: 100%;
        max-width: 900px;
    }

    .movie-detail {
        padding: 5px 0;
        
        h2 {
            color: #fff;
            font-size: 1.5em;
            font-weight: 600;
            margin-bottom: 16px;
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

    @media only screen and (max-width: 912px) {
        flex-wrap: wrap;
        top: -110px;
    }
}

        


</style>