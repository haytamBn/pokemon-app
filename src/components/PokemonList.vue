<template>
  <div class="container">
    <SimpleSelect
      :value="navigationType"
      v-model="navigationType"
      label="Navigation Type"
      @on-change-select="onChangeSelect($event)"
    />
    <div class="container-pokemon">
      <div v-show="isloading === true">Loading...</div>
      <div v-for="pokemon in pokemons" :key="pokemon.name">
        <PokemonCard
          :pokemnon-name="pokemon.name"
          :pokemon-height="pokemon.height"
          :pokemon-weight="pokemon.weight"
          :pokemon-img="pokemon.sprites.front_default"
        />
      </div>
    </div>
    <hr />
    <SimplePagination
      :navigation-type="navigationType"
      @prev-page="prevPage($event)"
      @next-page="nextPage($event)"
      :current-page="currentPage"
      :total-pages="totalPages"
    />
    <button
      v-if="navigationType === 'loadMore'"
      @click="loadMore"
      :disabled="pokemons.length >= 150"
    >
      Load more
    </button>
  </div>
</template>

<script>
import axios from "axios";

import PokemonCard from "./PokemonCard.vue";
import SimplePagination from "./SimplePagination.vue";
import SimpleSelect from "./SimpleSelect.vue";

export default {
  components: {
    PokemonCard,
    SimplePagination,
    SimpleSelect,
  },
  data() {
    return {
      pokemons: [],
      limit: 50,
      offset: 0,
      currentPage: 1,
      totalPages: 5,
      isloading: false,
      navigationType: "loadMore",
    };
  },
  mounted() {
    this.fetchPokemons();
  },
  methods: {
    async fetchPokemons() {
      this.isloading = true;
      const response = await axios.get(
        `https://pokeapi.co/api/v2/pokemon?limit=${this.limit}&offset=${this.offset}`
      );
      const pokemonPromises = response.data.results.map(async (pokemon) => {
        const pokemonData = await axios.get(pokemon.url);
        return pokemonData.data;
      });
      this.pokemons = [
        ...this.pokemons,
        ...(await Promise.all(pokemonPromises)),
      ];
      this.isloading = false;
    },
    loadMore() {
      if (this.navigationType === "loadMore") {
        this.limit = 15;
        this.offset += this.limit;
        this.fetchPokemons();
      }
    },
    onChangeSelect(value) {
      this.navigationType = value;
      if (this.navigationType !== "loadMore") {
        this.changePage(this.currentPage);
      }
    },
    async changePage(page) {
      this.currentPage = page;
      this.limit = 30;
      this.offset = (this.currentPage - 1) * 30;
      this.pokemons = [];
      await this.fetchPokemons();
    },
    nextPage() {
      if (
        this.navigationType === "pagination" &&
        this.currentPage < this.totalPages
      ) {
        this.changePage(this.currentPage + 1);
      }
    },
    prevPage() {
      if (this.navigationType === "pagination" && this.currentPage > 1) {
        this.changePage(this.currentPage - 1);
      }
    },
  },
};
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}

.container-pokemon {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 20px;
  flex-wrap: wrap;
  width: 100%;
}

button:disabled {
  background-color: #ccc;
  cursor: not-allowed;
}

button:disabled:active {
  background-color: #ccc;
  outline: 0;
}

button {
  align-items: center;
  background-color: white;
  border: 2px solid #111;
  border-radius: 8px;
  box-sizing: border-box;
  color: #111;
  cursor: pointer;
  display: flex;
  font-family: Inter, sans-serif;
  font-size: 16px;
  height: 35px;
  width: 180px;
  justify-content: center;
  line-height: 2px;
  max-width: 100%;
  padding: 0 15px;
  position: relative;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
}

button:after {
  background-color: #111;
  border-radius: 8px;
  content: "";
  display: block;
  height: 35px;
  left: 0;
  width: 100%;
  position: absolute;
  top: -2px;
  transform: translate(8px, 8px);
  transition: transform 0.2s ease-out;
  z-index: -1;
}

button:hover:after {
  transform: translate(0, 0);
}

button:active {
  background-color: white;
  outline: 0;
}

button:hover {
  outline: 0;
}

@media (min-width: 768px) {
  button {
    padding: 0 40px;
  }
}
</style>
