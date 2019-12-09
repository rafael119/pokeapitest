<template>
  <div id="app">
    <div class="hero is-success is-gradient is-bold">
      <div class="hero-body">
        <h1 class="title">
          <span class="has-text-warning">Pokedex</span>
        </h1>
        <span class="subtitle">Pokemon</span>
        <br>
        <div class="field has-addons is-pulled-right">
          <div class="control">
            <input
              v-model="search"
              type="text"
              class="input is-rounded"
              v-on:keyup.enter="searchData"
            >
          </div>
          <div class="control">
            <button class="button is-primary is-rounded" v-on:click="searchData">Buscar</button>
          </div>
        </div>
      </div>
    </div>
    <div class="container">
      <div class="columns is-desktop is-mobile is-tablet is-multiline is-centered">
        <pokemon
          @showModal="showModal"
          v-for="poke of pokemon"
          v-bind:key="poke.url"
          v-bind:poke="poke"
        />
      </div>

      <nav class="pagination" role="navegation" aria-label="pagination">
        <a class="pagination-previous" v-on:click=" changePage2(offset - 20)">Anterior</a>
        <ul class="pagination-list">
          <li>
            <a class="pagination-link is-current">{{offset}}</a>
          </li>
        </ul>
        <a class="pagination-previous" v-on:click=" changePage2(offset + 20)">Siguiente</a>
      </nav>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";
export default {
  name: "App",
  components: {
    Pokemon
  },
  data: function() {
    return {
      pokemon: [],
      pages: 1,
      offset: 0,
      search: ""
    };
  },
  created() {
    this.fetch();
  },
  methods: {
    fetch() {
      const params = {
        offset: this.offset,
        search: this.search
      };

      let result = axios
        .get("https://pokeapi.co/api/v2/pokemon", { params })
        .then(res => {
          this.pokemon = res.data.results;
          this.pages = res.data.count;
          console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    },
    fetch2() {
      let result = axios
        .get("https://pokeapi.co/api/v2/pokemon/" + this.search)
        .then(res => {
          this.pokemon = res.data.results;
          this.pages = res.data.count;
          console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    },
    changePage2(offset) {
      this.offset = offset < 0 || offset > this.pages ? this.offset : offset;
      this.fetch();
    },
    searchData() {
      this.offset = 0;
      this.fetch2();
    },
    showModal(id) {},

    fetch3() {}
  }
};
</script>
