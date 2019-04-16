<template>
  <v-card>
    <v-img :src="`./assets/${pokemon.originalId}${pokemon.name}.png`" height="200px" width="200px" class="white--text"></v-img>
    <v-card-title primary-title>
      <div class="data">
        <h3 class="headline mb-0">{{pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1)}}</h3>
        <ul>
            <li>{{pokemon.moves[0].name.charAt(0).toUpperCase() + pokemon.moves[0].name.slice(1)}}</li>
            <li>{{pokemon.moves[1].name.charAt(0).toUpperCase() + pokemon.moves[1].name.slice(1)}}</li>
            <li>{{pokemon.moves[2].name.charAt(0).toUpperCase() + pokemon.moves[2].name.slice(1)}}</li>
            <li>{{pokemon.moves[3].name.charAt(0).toUpperCase() + pokemon.moves[3].name.slice(1)}}</li>
        </ul>
      </div>
    </v-card-title>
  </v-card>
</template>

<script>
export default {
  props: {
    pokemon: {
      type: Object,
      required: true
    }
  }
};
</script>
<style scoped>
.data {
    margin: auto;
    text-align: center;
    background-color: #eee;
}
ul {
  list-style-type: none;
  padding: 10px;
}
</style>
