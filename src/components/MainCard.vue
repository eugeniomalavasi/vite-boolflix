<script>
import { store } from '../store.js'

export default {
    props: {
        card: Object,
        movie: String,
        series: String,
        cast: Object
    },
    data() {
        return {
            posterUrl: "https://image.tmdb.org/t/p/w342",
            moreInfo: false,
            store
        }
    },
    methods: {
        getImageUrl(imageName) {
            if (imageName === "it" || imageName === "fr" || imageName === "en" || imageName === "ja") {
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
        }, 
    }
}
</script>

<template>
    <div class="card">
        <div class="inner-card">

            <div class="card-front">
                <img :src="getPosterPath(card.poster_path)" class="poster" alt="">
            </div>

            <div class="card-back">
                <h3 v-if="movie">{{ card.title }}</h3>
                <h3 v-if="series">{{ card.original_name }}</h3>
                <p>{{ card.overview }}</p>
                <img class="flag" :src="getImageUrl(card.original_language)" alt="">
                <div>
                    <i class="fa-solid fa-star fullstar" v-for="num in roundNumb(card.vote_average)"></i>
                    <i class="fa-regular fa-star fullstar" v-for="num in 5 - roundNumb(card.vote_average)"></i>
                </div>
                <button @click="$emit('searchCast', card.id), moreInfo = !moreInfo"> More Info </button>
                <ul v-if="movie" class="extra-info">
                    <li v-if="moreInfo"> {{ this.store.castFilmArray[0].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castFilmArray[1].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castFilmArray[2].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castFilmArray[3].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castFilmArray[4].name}}</li>
                </ul>
                <ul v-if="series" class="extra-info">
                    <li v-if="moreInfo"> {{ this.store.castTvArray[0].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castTvArray[1].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castTvArray[2].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castTvArray[3].name}}</li>
                    <li v-if="moreInfo"> {{ this.store.castTvArray[4].name}}</li>
                </ul>
            </div>

        </div>
    </div>
</template>

<style lang="scss" scoped>
.card {
    background-color: transparent;
    height: 513px;
    width: 342px;
    perspective: 1000px;

    &:hover .inner-card {
        transform: rotateY(180deg);
    }

    .inner-card {
        position: relative;
        width: 100%;
        height: 100%;
        text-align: left;
        transition: transform 0.8s;
        transform-style: preserve-3d;

        .card-front,
        .card-back {
            position: absolute;
            width: 100%;
            height: 100%;
            -webkit-backface-visibility: hidden;
            backface-visibility: hidden;

            .fullstar {
                color: orange;
            }
        }

        .card-front {
            background-color: #bbb;
            color: black;
        }

        .card-back {
            background-color: lightgray;
            color: white;
            transform: rotateY(180deg);
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            gap: 1rem;
            padding: 1rem;

            h3 {
                color: orange;
                font-size: 2rem;
            }

            p {
                font-size: 0.7rem;
                color: black;
                font-weight: 600;
            }
        }
    }


}

.flag {
    width: 30px;
}
</style>