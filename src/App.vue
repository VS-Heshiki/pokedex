<template>
    <div id="app">
        <img src="./assets/LogoVSHeshiki.png" />
        <h1>Pokédex</h1>
        <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">Search!</span>
            <input type="text" class="form-control" v-model="search" />
        </div>
        <div class="container text-center">
            <div class="row row-cols-4">
                <div class="mt-5" v-for="poke in searchFiltered" :key="poke.url">
                    <pokemonPoke :name="poke.name" :url="poke.url" :id="poke.id" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    import pokemonPoke from './components/pokemonPoke.vue';
    export default {
        name: 'App',
        data() {
            return {
                search: '',
                pokemons: [],
            };
        },
        components: {
            pokemonPoke,
        },
        created() {
            axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res => {
                this.pokemons = res.data.results;
            });
        },
        computed: {
            searchFiltered: function () {
                if (this.search == '' || this.search == ' ') {
                    return this.pokemons;
                } else {
                    return this.pokemons.filter(pokemon => pokemon.name.toLowerCase() == this.search.toLowerCase());
                }
            },
        },
    };
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 40px;
    }

    h1 {
        margin-bottom: 5rem !important;
        color: #16213E;
    }

    .input-group {
        width: 30% !important;
        margin: auto;
    }
</style>
