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
        <div class="flex">
            <img src="../assets/Logonetflix.png" class="logo" alt="">
            <div>
                <input type="text" v-model="this.store.searchQuery" placeholder="ricerca" class="search">
                <button @click="$emit('search')">vai</button>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.container {
    height: 80px;
    background-color: black;
    margin-bottom: 3rem;

    .flex {
        align-items: center;
        height: 100%;
        width: 80%;
        margin: 0 auto;
        justify-content: space-between;

        .search {
            background-color: black;
            border-top: none;
            border-right: none;
            border-left: none;
            border-bottom: 1px solid white;
            cursor: pointer;
            color: white;
            padding: 5px;
        }
        button {
            background-color: black;
            color: white;
            border: 1px solid white;
            border-radius: 5px;
            padding: 5px 25px;
            margin-left: 1rem;
            cursor: pointer;
        }
    }

    .logo {
        width: 100px;
    }
}
</style>