<script>
export default {
  props: ["pokemnonName", "pokemonHeight", "pokemonWeight", "pokemonImg"],
};
</script>

<template>
  <div class="pokemon-card">
    <h3 class="title-card">{{ pokemnonName }}</h3>
    <hr />
    <img :src="pokemonImg" alt="pokemon" />
    <hr />
    <p><span>Height</span>: {{ pokemonHeight }} m</p>
    <p><span>Weight</span>: {{ pokemonWeight }} kg</p>
  </div>
</template>

<style>
h3 {
  text-transform: capitalize;
}

span {
  font-weight: bold;
}

.pokemon-card {
  display: flex;
  flex-direction: column;
  width: 150px;
  padding: 10px;
  border-radius: 5px;
  text-align: center;
  box-shadow: rgba(9, 30, 66, 0.25) 0px 1px 1px,
    rgba(9, 30, 66, 0.13) 0px 0px 1px 1px;
}
</style>
