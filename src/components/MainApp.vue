<script>
import { store } from '../store.js'
export default {
    data() {
        return {
            store,
        }
    },
}
</script>

<template>
    <div class="container">
        <div class="row">
            <div class="col" v-for="(card, i) in store.moviesArray">
                <div class="card">
                    <h3>{{ this.store.moviesArray[i].title }}</h3>
                    <h3>{{ this.store.moviesArray[i].vote_average }}</h3>
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
    
</style>