<script>
import { store } from './store.js'
import HeaderApp from './components/HeaderApp.vue'
import axios from 'axios'

export default {
  components: {
    HeaderApp,
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
        console.log('prendo la serie tv:', resp.data.results[0].name);
      })
    }
  },
}
</script>

<template>
  <div>
    <HeaderApp @search="getSeries" />
  </div>
</template>

<style lang="scss"></style>
