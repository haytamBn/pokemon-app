<template>
  <div id="app" class="app">
    <hr />
    <h1>Pokemon</h1>
    <hr />
    <PokemonList />
  </div>
</template>

<script>
import PokemonList from "./components/PokemonList.vue";

export default {
  components: {
    PokemonList,
  },
};
</script>

<style>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  padding: 30px;
  box-shadow: rgba(9, 30, 66, 0.25) 0px 1px 1px,
    rgba(9, 30, 66, 0.13) 0px 0px 1px 1px;
  border-radius: 5px;
}

hr {
  border-top: 1px solid #e2e8f0;
  width: 80%;
}
</style>
