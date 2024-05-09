<script>

export default {
    props: {
        card: Object,
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
    <div class="card">
        <img :src="getPosterPath(card.poster_path)" class="poster" alt="">
        <h3>{{ card.title }}</h3>
        <h3>{{ card.original_name }}</h3>
        <img class="flag" :src="getImageUrl(card.original_language)" alt="">
        <i class="fa-solid fa-star" v-for="num in roundNumb(card.vote_average)"></i>
        <i class="fa-regular fa-star" v-for="num in 5 - roundNumb(card.vote_average)"></i>
    </div>
</template>

<style lang="scss" scoped>
        .flag {
            width: 30px;
        }

</style>