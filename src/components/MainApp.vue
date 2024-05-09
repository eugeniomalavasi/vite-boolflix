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
            if (posterImg != null) {
                return new URL(`${this.posterUrl}${posterImg}`, import.meta.url).href;
            } else {
                return new URL("../assets/img-not-found.jpg", import.meta.url).href;
            }
        }, roundNumb(fractNumb) {
            return Math.ceil((fractNumb) / 2);
        }
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col" v-for="(movieCard, i) in store.moviesArray">
                <div class="card">
                    <img :src="getPosterPath(movieCard.poster_path)" class="poster" alt="">
                    <h3>{{ movieCard.title }}</h3>
                    <h3>original name: {{ movieCard.original_name }}</h3>
                    <img class="flag" :src="getImageUrl(movieCard.original_language)" alt="">
                    <i class="fa-solid fa-star" v-for="num in roundNumb(movieCard.vote_average)"></i>
                    <i class="fa-regular fa-star" v-for="num in 5 - roundNumb(movieCard.vote_average) "></i>
                </div>
            </div>
            <div class="col" v-for="(seriesCard, i) in store.seriesArray">
                <div class="card">
                    <img :src="getPosterPath(seriesCard.poster_path)" alt="">
                    <h3>title: {{ seriesCard.name }}</h3>
                    <h3>original name: {{ seriesCard.original_name }}</h3>
                    <img class="flag" :src="getImageUrl(seriesCard.original_language)" alt="">
                    <i class="fa-solid fa-star" v-for="num in roundNumb(seriesCard.vote_average)"></i>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.row {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;

    .col {
        width: 33%;

        .flag {
            width: 30px;
        }
    }

}
</style>