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
    <div>
        <input type="text" v-model="this.store.searchQuery">
        <button @click="$emit('search')">vai</button>
    </div>
</template>

<style lang="scss" scoped>


</style>