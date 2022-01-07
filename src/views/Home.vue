<template>
    <div class="home">
        <header>
            <div class="bg-header"></div>
            <div class="content-header">
                <h1>Lou<span>Z</span></h1>

                <h3>Are you looking for watch a movie or serie?</h3>

                <form @submit.prevent="SearchMovies()" class="search-box">
                    <input type="text" placeholder="Search..." v-model="search">
                    <input type="submit" value="Search">
                </form>
            </div>
        </header>

        <div class="movies-list">
            <div class="movie" v-for="movie in movies" :key="movie.imdbID">
                <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
                    <div class="product-image">
                        <img :src="movie.Poster" alt="Movie Poster">
                        <div class="type">{{ movie.Type }}</div>
                    </div>
                    <div class="detail">
                        <p class="year">{{ movie.Year }}</p>
                        <h3>{{ movie.Title }}</h3>
                    </div>
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>
import { ref  } from "vue";
import env from '@/env.js'

export default {
  name: "Home",
  
  setup() {
    const search = ref("");
    const movies = ref([]);

    const SearchMovies = () => {
      if(search.value != "") {
        //console.log(search.value);
        fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`).then(response => response.json()).then(data => {
          movies.value = data.Search;
          search.value = "";
          //console.log(movies.value)
        })
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style lang="scss">

    //colors
    $color1: #357ded;
    $color2: #151515;
    $color3: #32e875;
    $color4: #e1e5ee;
    $color5: #5438dc;

    .home {
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
                filter: blur(4px);
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
                text-align: center;

                h1 {
                    color: $color3;
                    font-size: 3.4em;
                    margin-bottom: 15px;
                    text-shadow: 1px 1px 10px rgba(0, 0, 0, .8);

                    span {
                        color: $color4;
                    }
                }

                h3 {
                    color: $color4;
                    font-size: 1.3em;
                    margin-bottom: .8em;
                    font-weight: 400;

                    @media only screen and (max-width: 575.98px) {
                        margin: 0 10px;
                    }
                }
                
                form {
                    display: flex;
                    flex-direction: row;
                    justify-content: center;
                    align-items: center;

                    input {
                        display: block;
                        appearance: none;
                        border: none;
                        outline: none;
                        background-color: none;
             
                        &[type="text"] {
                            background-color: $color4;
                            width: 100%;
                            max-width: 300px;
                            font-size: 1.2em;
                            padding: 10px 16px;
                            border-radius: 8px;
                            margin-bottom: 15px;
                            transition: 0.4s;
                            margin-top: 13px;
                            margin-right: 10px;


                            &::placeholder {
                                color: $color2;
                            }
                            
                            &:focus {
                                box-shadow: 0px 3px  6px rgba(0,0,0,0.2);
                            }

                            @media only screen and (max-width: 575.98px) {
                                font-size: 1.1em;
                                margin-right: 0;
                            }
                        }

                        &[type="submit"] {
                            max-width: 300px;
                            background-color: rgba($color: #000000, $alpha: 0);
                            padding: 10px 25px;
                            border-radius: 50px;
                            color: $color4;
                            border: 4px solid;
                            font-size: 1.2em;
                            text-transform: uppercase;
                            transition: 0.4s;

                            &:active {
                                background-color: #3b8070;
                            }

                            @media only screen and (max-width: 575.98px) {
                                font-size: 1em;
                                width: 100%;
                            }
                        }
                        
                    }

                    @media only screen and (max-width: 575.98px) {
                        flex-wrap: wrap;
                        padding: 0 7px;
                    }

                }
            }
        }

        .movies-list {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin: 0px 8px;

            .movie {
                max-width: 200px;
                flex: 1 1 50%;
                padding: 16px 8px;

                .movie-link {
                display: flex;
                flex-direction: column;
                height: 100%;
                box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
                transition: .2s;
                
                    .product-image {
                        position: relative;
                        display: block;

                        img {
                        display: block;
                        width: 100%;
                        height: 275px;
                        object-fit: cover;
                        }

                        .type {
                            position: absolute;
                            padding: 8px 16px;
                            background-color: $color5;
                            color: $color4;
                            bottom: 16px;
                            left: 0;
                            text-transform: capitalize;
                        }
                    }

                    .detail {
                        background-color: $color1;
                        padding: 16px 8px;
                        flex: 1 1 100%;
                        border-radius: 0px 0px 8px 8px;

                        .year {
                        color: $color3;
                        font-size: .85em;
                        font-weight: bold;
                        }

                        h3 {
                        color: $color4;
                        font-weight: 600;
                        font-size: 1em;
                        }
                    }

                    &:hover {
                        margin-top: 10px;
                    }
                }
            }
        }
    }
</style>