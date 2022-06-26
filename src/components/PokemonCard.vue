<template>
  <div>
    <div id="searchForNewPokemonDiv">
      <button id="searchForNewPokemonBtn" @click="closeDetail" class="close" >click here to search for new pokemon</button>
    </div>
    <div id="spinner" class="shiny detailView pokemonCard" v-if="showDetail">
      <div v-if="pokemon" class="data">
            <h2 id="pokemonName">{{ pokemon.name }}</h2>
            <img style="border: 0.2rem solid var(--color);" :src="image" alt=""/>
             
           <!-- Adds the female picture -->
           <!-- <span v-if="imageFemale !== null" >
                <p>Female</p>
                <img :src="imageFemale" alt=""/>
            -->
        
          <h2 id="pokemonElement">{{ pokemonElement}}</h2>
        <div id="pokemonStats">
          <h3 style="font-family:fantasy">Stats</h3>
          <li v-for="stat in pokemon.stats">
            <span>{{ stat.stat.name }}: </span>
            <span>{{ stat.base_stat }}</span>
          </li>
        </div>
        <div id="pokemonMoves">
        <h3 style="font-family:fantasy" >Moves</h3>
          <ul id="pokemonMovesUl">         
            <li v-for="stat in pokemon.moves">
              <span>{{ stat.move.name }}</span>
            </li>
          </ul>
        </div>
        <h3 style="font-family:fantasy" >Abilities</h3>
        <div class="abilities">
          <div class="ability" 
            v-for="(value, index) in pokemon.abilities"
            :key="'value'+index">
            {{ value.ability.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
  <h2 v-if="pokemonNotFound" style="font-size: 4rem; font-family:Arial, Helvetica, sans-serif ">The pokemon was not found, try again</h2>
  <div style="margin: 7rem auto" v-if="loading" class="loader">
  </div>
</template>

<script>

  export default {
    props: [
      'pokemonUrl',
    ],
    data: () => {
      return {
        showDetail: false,
        pokemon: {},        
        image: '',
        imageFemale: '',
        pokemonElement: '',
        pokemonColor: '',
        loading: true,
        pokemonNotFound: false,
      }      
    },
    methods: {
        fetchData() {
        let req = new Request(this.pokemonUrl);
        fetch(req)
          .then((response) => {
            if(response.status === 200)
              this.loading = false;
              return response.json();
          })
          .then((data) => {
            this.pokemon = data;
            this.image = data.sprites.front_default;
            this.imageFemale = data.sprites.front_female;
            this.showDetail = true;
            // get type name from data map 
            this.pokemonElement = data.types.map(({ type }) => type.name.toString()).join(', ');
            document.documentElement.style.setProperty('--color', this.determineElementColor(this.pokemonElement)
            );
          })    
          .catch((error) => {
            console.log(error);
            this.$emit('pokemonNotFound', this.pokemonNotFound);
            this.closeDetail();
          })
      },
      determineElementColor(element) {
        
        if(element === 'fire' 
              || element === 'fighting') 
          return 'red';
        else if( element == 'electric')
          return 'yellow';
        else if( element == 'water' 
              || element == 'ice' 
              || element == 'flying'
              || element == 'dragon')
          return 'blue'; 
        else if( element == 'grass' 
              || element == 'bug') 
          return 'green';
        else if( element== 'poison' 
              || element == 'psychic'
              || element== 'ghost' 
              || element == 'dark')
          return 'purple';
        else if( element == 'ground' 
              || element == 'rock' 
              || element == 'steel') 
          return 'brown';
        else if( element == 'fairy')
          return 'pink';
        else
          return 'black';
      },
      closeDetail() {
        this.$emit('closeDetail');
      }
    },
    created() {
      this.fetchData();
    }
  }
</script>

<style>

#searchForNewPokemonDiv {
/* center button in the middle of the screen */
  padding-top: 1rem;
  text-align: center;  
}

#searchForNewPokemonBtn {
  font-size: 1rem;
  font-family: 'Trebuchet MS';
  color: white;
  border: 0.1rem solid rgb(255, 255, 255);
  border-radius: 0.5rem;
  padding: 0.5rem;
  margin: 0.5rem;
  cursor: pointer;
  box-shadow:
    inset 0 0 50px #fff,
    inset 20px 0 80px rgb(252, 126, 252),
    inset -20px 0 80px #0ff,
    inset 20px 0 300px #f0f,
    inset -20px 0 300px #0ff,
    0 0 50px #fff,
    -10px 0 80px #f0f,
    10px 0 80px #0ff;  
}
/* import cool font from google, pokemon font  */

.pokemonCard {
    -webkit-font-smoothing: antialiased;
    text-rendering: optimizeLegibility;
    font-size: 1rem;
    color: #fff8fa;
    box-sizing: inherit;
    width: 25rem;
    height: 40rem;
    border: 1rem  black;
    text-align: center;
    padding: 1rem;
    margin: 5rem auto;
    background: #FFF;
    box-shadow: 1px 1px 3px #000;
    border-radius: 1.5rem;
    background-size: 400% 400%;
    background: linear-gradient(45deg, rgb(255, 166, 0), purple, red, blue);
    box-shadow:
    inset 0 0 50px #fff,
    inset 20px 0 80px #f0f,
    inset -20px 0 80px #0ff,
    inset 20px 0 200px #f0f,
    inset -20px 0 300px #0ff,
    0 0 50px #fff,
    -10px 0 80px #f0f,
    10px 0 80px #0ff;
    transition: all 2s;

}


.pokemonCard:hover {
    box-shadow:
    inset 0 0 50px #fff,
    inset 20px 0 80px #f0f,
    inset -20px 0 80px #0ff,
    inset 20px 0 70px #f0f,
    inset -20px 0 240px #0ff,
    0 0 50px #fff,
    -10px 0 80px #f0f,
    10px 0 80px #0ff;
    transform: 
    rotate3d(100, -180, 200, -8deg) ;
}

.shiny::after {
    content: '';
    display: block;
    width: 70%;
    background: rgba(255, 255, 255, 0.2);
    background: linear-gradient(0deg, rgba(255, 255, 255, 0.2)50%, rgba(255, 255, 255, 0.7)100%); /* Safari 5.1-6.0 */
    background: -o-linear-gradient(0deg, rgba(255, 255, 255, 0.2)50%, rgba(255, 255, 255, 0.7)100%); /* Opera 11.1-12.0 */ 
    background: -moz-linear-gradient(0deg, rgba(255, 255, 255, 0.2)50%, rgba(255, 255, 255, 0.7)100%); /* Firefox 3.6-15 */
    background: linear-gradient(0deg, rgba(255, 255, 255, 0.2)50%, rgba(255, 255, 255, 0.7)100%); /* Standard syntax */
    left: -200%;
    top: 0;
    height: 100%;
    position: absolute;
    transition: none;
    -webkit-transition: none;
    -moz-transition: none;
    -o-transition: none;
    -ms-transition: none;
    -ms-transform: skewX(-20deg); /* IE 9 */
    -webkit-transform: skewX(-20deg); /* Safari */
    transform: skewX(-20deg);
}

.shiny:hover::after {
    left: 150%;
    transition: all 1s;
    -webkit-transition: all 1s;
    -moz-transition: all 1s;
    -o-transition: all 1s;
    -ms-transition: all 1s;
}

h1,h2,h3, p {
  text-align: center;
  /* text color is linear gradient primarily white */
}

#pokemonName {
  font-size: 2rem;
  font-weight: bold;
  color: #fff8fa;
  font-family: Pokemon Go Solid;
}

#pokemonElement {
  color: var(--color);
}

#pokemonMovesUl {
  width: 23.2rem;
  height: 3rem; 
  overflow: auto;
}

/* custom scrollbar start*/
::-webkit-scrollbar {
  width: 40px;
  
}

::-webkit-scrollbar-track {
  background-color: #f1f1f1;

}

::-webkit-scrollbar-thumb {
  background-color: var(--color);
  border-radius: 20px;
  border: 6px solid transparent;
  background-clip: content-box;
}

::-webkit-scrollbar-thumb:hover {
  background-color: #a8bbbf;
}
/* custom scrollbar stop */

.loader {
  width:40px;
  height:40px;
  border-radius: 50%;
  border:4px solid;
  position: relative;
  transform-origin: left;
  animation: loader 1s infinite linear;
}
.loader::before,
.loader::after {
  content: "";
  position: absolute;
  inset:0 0 auto;
  margin:auto;
  width:30%;
  height:30%;
  border-radius: 50%;
  border:4px solid;
  transform-origin: 50% calc(100% - 6px);
  animation: inherit;
}
@keyframes loader{
  100% {transform:rotate(360deg)}
}

body {
  overflow: hidden; /* Hide scrollbars */
}

  
</style>

