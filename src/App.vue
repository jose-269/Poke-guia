<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-12 my-5 text-center">
          <img src="https://raw.githubusercontent.com/PokeAPI/media/master/logo/pokeapi_256.png" alt="">
        </div>
        <div class="col-12 text-center mb-5">
          <h1>PokeGuia</h1>
        </div>
      </div>
        <div class="row mb-5">
          <div class="col-12 text-center">
            <div class="form-group">
              <label class="form-label fs-4 m-0 text-center">Nombre:</label>
              <input type="text" class="form-control-sm mx-2 border border-primary" placeholder="" v-model="pokeName" v-on:keyup.enter="getPoke">
              <button type="button" class="btn btn-primary py-1" @click="getPoke" v-on:keyup.enter="getPoke">Buscar</button>
            </div>
          </div>
        </div>
        <div class="row text-center">
          <div class="col-12 mb-5">
            <img :src="pokemons && pokemons.sprites && pokemons.sprites.front_default" alt="Pokemon-front">
          </div>
        </div>
        <div class="row text-center">
          <div class="col-sm-12 col-md-6">
            <h2 class="mb-3">Movimientos</h2>
            <ul class="p-0">
              <li class="p-0" v-for="(poder, i) in pokemons.moves" :key="i">
                {{ poder.move.name }}
              </li>
            </ul> 
          </div>
          <div class="col-sm-12 col-md-6">
            <h2 class="mb-3">Habilidades</h2>
            <ul class="p-0">
              <li  v-for="(caract, i) in pokemons.abilities" :key="i">
                {{ caract.ability.name }}
              </li>
            </ul>
          </div>
        </div>
      
    </div>
    <Poke />
  </div>
</template>

<script>
import Poke from "./components/Poke.vue";
import axios from "axios";
export default {
  name: "App",
  components: {
    Poke,
  },
  data() {
    return {
      pokemons: "",
      pokeName: "pikachu",
    }
  },
  created () {
    this.getPoke();
  },
  methods: {
    async getPoke() {
      const url = "https://pokeapi.co/api/v2/pokemon/";
      try {
        const req = await axios(url + this.pokeName.toLowerCase());
        if(!req) return;
        this.pokemons = req.data;
        console.log(req.data);
      } catch (error) {
        console.log(error);
      }
    }
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
ul>li {
  list-style: none;
}
</style>
