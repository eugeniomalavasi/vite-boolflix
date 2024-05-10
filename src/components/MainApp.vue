<script>
import { store } from '../store.js'
import MainCard from './MainCard.vue'
import axios from 'axios';

export default {
    data() {
        return {
            store,
            series: "series",
            movie: "movie"
        }
    }, methods: {
        getFilmCast(movieId = 495438) {
            console.warn(movieId);
            axios
                .get(`https://api.themoviedb.org/3/movie/${movieId}/credits`, {
                    params: {
                        api_key: this.store.apiKey,
                    }
                })
                .then((resp) => {
                    this.store.castFilmArray = resp.data.cast;
                    console.log("array attori:", this.store.castFilmArray);
                })
        },
        getTvCast(tvId = 495438) {
            console.warn(tvId);
            axios
                .get(`https://api.themoviedb.org/3/tv/${tvId}/credits`, {
                    params: {
                        api_key: this.store.apiKey,
                    }
                })
                .then((resp) => {
                    this.store.castTvArray = resp.data.cast;
                    console.log("array attori:", this.store.castTvArray);
                })
        }
    }, components: {
        MainCard,
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col" v-for="card in store.moviesArray">
                <MainCard :card="card" :movie="movie" @searchCast="getFilmCast" />
            </div>
            <div class="col" v-for="card in store.seriesArray">
                <MainCard :card="card" :series="series" @searchCast="getTvCast"/>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 1rem;
}
</style>