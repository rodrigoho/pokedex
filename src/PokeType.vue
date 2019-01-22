<template>
    <div class="poke-type">
         <p class="poke-type" v-for="pokeType in pokeTypes" :key="pokeType.id">{{ pokeType.type.name }}</p>
    </div>
</template>

<script>
import axios from 'axios';
import PokeCard from './PokeCard';

export default {
    name: 'pokeType',
    props: {
        pokemonName: {
            type: String,
            required: true,
        },
    },
    data() {
        return {
            pokeTypes: [],
            nextPokemon: '',
        };
    },
    created(){
        this.loadPokemonType(`https://pokeapi.co/api/v2/pokemon/${this.pokemonName}`);
    },
    methods: {
        loadPokemonType(url) {
            axios.get(url).then(response => {
                response.data.types.forEach(pokeType => {
                    this.pokeTypes.push(pokeType);
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

