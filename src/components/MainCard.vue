<script>

export default {
    props: {
        seriesCard: Object,
        movieCard: Object,
        movie: String,
        series: String
    },
    data() {
        return {
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
    <div class="card" v-if="seriesCard">
        <img :src="getPosterPath(seriesCard.poster_path)" alt="">
        <h3>{{ seriesCard.name }}</h3>
        <h3>{{ seriesCard.original_name }}</h3>
        <img class="flag" :src="getImageUrl(seriesCard.original_language)" alt="">
        <i class="fa-solid fa-star" v-for="num in roundNumb(seriesCard.vote_average)"></i>
        <i class="fa-regular fa-star" v-for="num in 5 - roundNumb(seriesCard.vote_average)"></i>
    </div>

    <div class="card" v-if="movieCard">
        <img :src="getPosterPath(movieCard.poster_path)" class="poster" alt="">
        <h3>{{ movieCard.title }}</h3>
        <h3>{{ movieCard.original_name }}</h3>
        <img class="flag" :src="getImageUrl(movieCard.original_language)" alt="">
        <i class="fa-solid fa-star" v-for="num in roundNumb(movieCard.vote_average)"></i>
        <i class="fa-regular fa-star" v-for="num in 5 - roundNumb(movieCard.vote_average)"></i>
    </div>
</template>

<style lang="scss" scoped>
        .flag {
            width: 30px;
        }

</style>