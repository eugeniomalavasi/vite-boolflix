<script>
import { store } from '../store.js'
import MainCard from './MainCard.vue'

export default {
    data() {
        return {
            store,
            series: "series",
            movie: "movie"
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
            <div class="col" v-for="(card, i) in store.moviesArray">
                <MainCard :card="card" :movie="movie"/>
            </div>
            <div class="col" v-for="(card, i) in store.seriesArray">
                <MainCard :card="card" :series="series" />
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