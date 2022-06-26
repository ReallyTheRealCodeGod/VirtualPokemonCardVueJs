<script >
    export default {

        props: [
            'apiUrl',
            'NotFound'
        ],
        data() {
            return {
                searchValue: '',    
            }
        },
        methods: {
        setPokemonUrl(url) {
            if(this.searchValue !== ''){
            //change
            this.searchValue = this.searchValue.toLowerCase().trim();
            this.$emit('setPokemonUrl', this.apiUrl + this.searchValue);
        }
        }

    }
}

</script>
    <template>



        <div id="cover">
 
    <div class="tb">
      <div class="td">
        <form @submit.prevent="setPokemonUrl" > 
            <input type="text" v-model="searchValue" placeholder="Search for pokemon" required/>
        </form>
      </div>
      <div class="td">
        <button @click="setPokemonUrl" class="gg-pokemon" type="submit">
          <div id="s-circle"></div>
          <span></span>
        </button>
      </div>
    </div>

</div>

<div v-if="NotFound">
<h1>the pokemon was not found, try again</h1>
</div>

    </template>

<style>

@import url('https://css.gg/pokemon.css');

*{
    cursor: url(https://cur.cursors-4u.net/games/gam-13/gam1309.ani), url(https://cur.cursors-4u.net/games/gam-13/gam1309.png), auto !important;
    outline: none;
    }


.gg-pokemon {
    box-sizing: border-box;
    position: relative;
    display: block;
    transform: scale(2);
    width: 18px;
    height: 18px;
    border: 5px solid transparent;
    box-shadow:
        0 0 0 2px,
        inset 0 0 0 2px;
    border-radius: 100%
}

.gg-pokemon::before {
    content: "";
    display: block;
    box-sizing: border-box;
    position: absolute;
    width: 20px;
    height: 2px;
    border-left: 8px solid;
    border-right: 8px solid;
    left: -6px;
    top: 3px
}


.td {
  display: table-cell;
  vertical-align: middle;
}

.tb {
  display: table;
  width: 100%;
}

#cover {
  position: absolute;
  top: 50%;
  left: 0;
  right: 0;
  width: 50rem;
  padding: 35px;
  margin: -4rem auto 0 auto;
  background-color: #e6e7ff;
  border-radius: 20px;
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


input[type="text"] {
  width: 100%;
  height: 96px;
  font-size: 4rem;
  line-height: 1;
}

input[type="text"]::placeholder {
  color: #ffffff;
    font-size: 3.5rem;
}


</style>
