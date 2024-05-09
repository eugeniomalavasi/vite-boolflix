<script>
import { store } from './store.js'
import HeaderApp from './components/HeaderApp.vue'
import MainApp from './components/MainApp.vue'
import axios from 'axios'

export default {
  components: {
    HeaderApp,
    MainApp
  },
  data() {
    return {
      store,
    }
  }, methods: {
    getSeries() {
      axios
      .get("https://api.themoviedb.org/3/search/tv", {
        params: {
          api_key: this.store.apiKey,
          query: this.store.searchQuery,
        }
      })
      .then((resp)=> {
        this.store.seriesArray = resp.data.results
        console.log(this.store.seriesArray);
      })
    },
    getMovies() {
      axios
      .get("https://api.themoviedb.org/3/search/movie", {
        params: {
          api_key: this.store.apiKey,
          query: this.store.searchQuery,
        }
      })
      .then((resp)=> {
        this.store.moviesArray = resp.data.results
        console.log(this.store.moviesArray);
      })
    }
  },
}
</script>

<template>
  <div>
    <HeaderApp @search="{getSeries(); getMovies()}" @keyup.enter="{getSeries(); getMovies()}" />
    <MainApp />
  </div>
</template>

<style lang="scss"></style>
