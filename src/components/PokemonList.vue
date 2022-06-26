<script >


</script>

<template>

<!-- make button that fetches the pokemons when clicked -->
<button @click="fetchPokemons">Fetch Pokemons</button>

    <div id="app">
        <div v-if="loading">
        <p>Loading...</p>
        </div>
        <div v-else>
        <ul>
            <li v-for="pokemon in pokemons">
            <a href="#" @click="showPokemon(pokemon)">
                {{ pokemon.name }}
            </a>
            </li>
                <!-- div that shows the abilities of the pokemon, that has just been clicked -->
                <!-- show abilities in another column -->

    
        <div id="pokeDetails" v-if="pokemonShown" @click="this.pokemonShown = !this.pokemonShown">

            <ul>
                <li v-for="ability in abilities">
                    <!-- get ability name and url from array-->
                    <h1>{{ ability.abilityNames }}</h1>
                    <h1>{{ ability.abilityUrls }}</h1>
                </li>
            </ul>
            <!-- get pokemon image and display it -->
            <img id="pokeDetailImage" :src="image" alt="pokemon" />
        </div>
        </ul>
        </div>
    </div>    

  
</template>

<style>

</style>
