<template>
    <div class="poke-card">
        <h2>#{{ pokemonId }} {{ pokemon.name }} {{  }}</h2>
        <img :src="imgSrc"/>
        <poke-type
            :pokemonName="pokemon.name"
            :key="pokemon.name"/>
    </div>    
</template>

<script>
import VueCollapse from 'vue2-collapse'
import PokeType from './PokeType'
// Vue.use(VueCollapse);
export default {
    name: 'pokeCard',
    props: {
        pokemon: {
            type: Object,
            required: true,
        },
    },
    computed: {
        imgSrc() {
            return `https://img.pokemondb.net/sprites/black-white/normal/${this.pokemon.name}.png`;
        },
        pokemonId() {
            const url = this.pokemon.url.split('/');
            url.pop();
            return url[url.length - 1];
        }
    },
    components: {
        PokeType,
    }
}
</script>

<style>
.poke-card {
  padding: 5px;
  margin: 10px;
  min-height: 40px;
  width: 20vw;
  height: 17vw;
  box-shadow: 0 0 10px rgb(25, 0, 255);
  text-transform: uppercase;
  text-align: center;
}
.poke-card h2 {
  margin: 0;
  margin-top: 5px;
}
</style>
