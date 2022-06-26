<script>
import PokemonSearch from "./components/PokemonSearch.vue";
import PokemonCard from "./components/PokemonCard.vue";

export default {

    components: {
    PokemonSearch,
    PokemonCard
},
   
    data() {
        return {
            apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
            displayCard: false,
            pokemonUrl: '',
            NotFound: false,
        }
    },
    methods: {
      setPokemonUrl(url) {
            this.pokemonUrl = url;
            this.displayCard = true; 
            this.NotFound = false;
        },
      closeDetail() {
        this.pokemonUrl = '';
        this.displayCard = false;
      },
      pokemonNotFound() {
        this.NotFound = true;
      }
    },
    mounted() {
        this.pokemonUrl = this.apiUrl + 'pikachu';
        this.displayCard = true;
    }
}

</script>

<template>

        <PokemonSearch
          v-if="!displayCard"
          :apiUrl="apiUrl" 
          :NotFound="NotFound"
          @setPokemonUrl="setPokemonUrl"

        />
        <PokemonCard 
          v-if="displayCard"
          :pokemonUrl="pokemonUrl"
          @pokemonNotFound="pokemonNotFound"
          @closeDetail="closeDetail"
        ></PokemonCard>

</template>

<style>

form {
  height: 6rem;
}

body {
  margin: 0;
  background-color: #ffffff;
  overflow: hidden; /* Hide scrollbars */
}

input,
button {
  color: rgba(33, 29, 255, 0.616);
  padding: 0;
  margin: 0;
  border: 0; 
  background-color: transparent;
  transition: all 0.3s ease-in-out;
}

button:hover {
  transform:  scale(1.2);;

}

li {
  list-style-type: none;
}

</style>
