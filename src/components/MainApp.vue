<script>
import { store } from '../store.js'
export default {
    data() {
        return {
            store,
            posterUrl: "https://image.tmdb.org/t/p/w342",
        }
    }, methods: {
        getImageUrl(imageName) {
            if (imageName === "it" || imageName === "fr" || imageName === "en") {
                return new URL(`../assets/${imageName}.png`, import.meta.url).href;
            } else {
                return new URL(`../assets/rest.png`, import.meta.url).href;
            }
        }, getPosterPath(posterImg) {
            return new URL(`${this.posterUrl}${posterImg}`, import.meta.url).href;
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col" v-for="(movieCard, i) in store.moviesArray">
                <div class="card">
                    <img :src="getPosterPath(movieCard.poster_path)" alt="">
                    <!-- <img :src="posterUrl + movieCard.poster_path" alt=""> -->
                    <h3>{{ movieCard.title }}</h3>
                    <h3>original name: {{ movieCard.original_name }}</h3>
                    <p>vote: {{ movieCard.vote_average }}</p>
                    <img class="flag" :src="getImageUrl(movieCard.original_language)" alt="">
                </div>
            </div>
            <div class="col" v-for="(seriesCard, i) in store.seriesArray">
                <div class="card">
                    <h3>title: {{ seriesCard.name }}</h3>
                    <h3>original name: {{ seriesCard.original_name }}</h3>
                    <p>vote: {{ seriesCard.vote_average }}</p>
                    <img class="flag" :src="getImageUrl(seriesCard.original_language)" alt="">
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.flag {
    width: 30px;
    max-width: 100%;
}
</style>