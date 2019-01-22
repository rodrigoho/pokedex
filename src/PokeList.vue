<template>
    <div class="poke-list">
        <poke-card v-for="pokemon in pokemons"
            :pokemon="pokemon"
            :key="pokemon.name"/>

        <button @click="loadPokemons(nextPage)">
            Carregar mais
        </button>
    </div>
</template>

<script>
import axios from 'axios';
import PokeCard from './PokeCard';

export default {
    name: 'pokeList',
    components: {
        PokeCard,
    },
    data() {
        return {
            pokemons: [],
            nextPage: '',
        };
    },
    created(){
        this.loadPokemons('https://pokeapi.co/api/v2/pokemon/');
    },
    methods: {
        loadPokemons(url) {
            axios.get(url).then(response => {
                response.data.results.forEach(pokemon => {
                    this.pokemons.push(pokemon);
                });
                this.nextPage = response.data.next;
            }).catch(err => alert('Error!', err));
        },
    },    
}
</script>
<style>
.poke-list {
  display: flex;
  justify-content: center;
  align-items: center;
  max-width: 80vw;
  margin: auto;
  flex-wrap: wrap;
}

.poke-list button {
  position: fixed;
  border-radius: 2px;
  font-size: 16px;
  padding: 10px;
  text-transform: uppercase;
  top: 30px;
  right: 30px;
  background-color: transparent;
  border: 1px solid rgb(25, 0, 255);
  cursor: pointer;
}

.poke-list button:hover {
  background-color: rgb(25, 0, 255);
  color: white;
}
</style>

