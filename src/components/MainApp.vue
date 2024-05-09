<script>
import { store } from '../store.js'
import MainCard from './MainCard.vue'

export default {
    data() {
        return {
            store,
            // posterUrl: "https://image.tmdb.org/t/p/w342",
        }
    }, methods: {

    }, components: {
        MainCard,
    }
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col" v-for="(movieCard, i) in store.moviesArray">
                <MainCard :movieCard="movieCard" />
            </div>
            <div class="col" v-for="(seriesCard, i) in store.seriesArray">
                <MainCard :seriesCard="seriesCard"  />
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