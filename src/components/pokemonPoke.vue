<template>
    <div>
        <div class="card border-dark" style="width: 18rem">
            <div class="pokeImg">
                <img :src="frontImage" class="card-img-top" />
                <img :src="backImage" class="card-img-top" />
            </div>
            <div class="btn-group" role="group" aria-label="Basic example">
                <button type="button" class="btn btn-primary" @click="normal">Normal</button>
                <button type="button" class="btn btn-primary" @click="shiny">Shiny</button>
            </div>
            <div class="card-body">
                <h5 class="card-title">{{ pokemon.id }} - {{ upper(name) }}</h5>
                <p class="card-text" :class="pokemon.type1">{{ pokemon.type1 }}</p>
                <p class="card-text" :class="pokemon.type2">{{ pokemon.type2 }}</p>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                isNormal: true,
                frontImage: '',
                backImage: '',
                pokemon: {
                    id: '',
                    type: '',
                    type1: '',
                    type2: '',
                    front: '',
                    back: '',
                    frontShiny: '',
                    backShiny: '',
                },
            };
        },
        created() {
            axios.get(this.url).then(res => {
                this.pokemon.id = res.data.id;
                this.pokemon.front = res.data.sprites.front_default;
                this.pokemon.back = res.data.sprites.back_default;
                this.pokemon.frontShiny = res.data.sprites.front_shiny;
                this.pokemon.backShiny = res.data.sprites.back_shiny;
                this.frontImage = this.pokemon.front;
                this.backImage = this.pokemon.back;
                this.pokemon.type1 = res.data.types[0].type.name.toUpperCase();
                this.pokemon.type2 = res.data.types[1].type.name.toUpperCase();
            });
        },
        props: {
            name: String,
            url: String,
            id: Number,
        },
        methods: {
            upper: function (value) {
                var upper = value[0].toUpperCase() + value.slice(1);
                return upper;
            },
            normal: function () {
                this.isNormal = true;
                this.frontImage = this.pokemon.front;
                this.backImage = this.pokemon.back;
            },
            shiny: function () {
                this.isNormal = false;
                this.frontImage = this.pokemon.frontShiny;
                this.backImage = this.pokemon.backShiny;
            },
        },
    };
</script>

<style>
    .card {
        border-radius: 9px !important;
        background-color: #b1b2ff !important;
        height: 20rem !important;
    }

    .btn-group {
        width: 50%;
        margin: auto !important;
    }

    .pokeImg {
        display: flex;
        justify-content: space-around;
    }

    .card-text {
        border-radius: 9px !important;
        font-weight: 600;
    }

    .GRASS {
        background-color: #7ac74c;
    }

    .NORMAL {
        background-color: #a8a77a;
    }

    .FIRE {
        background-color: #ee8130;
    }

    .WATER {
        background-color: #6390f0;
    }

    .ELECTRIC {
        background-color: #f7d02c;
    }

    .ICE {
        background-color: #96d9d6;
    }

    .FIGHTING {
        background-color: #c22e28;
    }

    .POISON {
        background-color: #a33ea1;
    }

    .GROUND {
        background-color: #e2bf65;
    }

    .PSYCHIC {
        background-color: #f95587;
    }

    .BUG {
        background-color: #a6b91a;
    }

    .ROCK {
        background-color: #b6a136;
    }

    .GHOST {
        background-color: #735797;
    }

    .DRAGON {
        background-color: #6f35fc;
    }

    .FAIRY {
        background-color: #d685ad;
    }

    .STEEL {
        background-color: #b7b7ce;
    }

    .DARK {
        background-color: #705746;
    }

    .FLYING {
        background-color: #a98ff3;
    }
</style>
