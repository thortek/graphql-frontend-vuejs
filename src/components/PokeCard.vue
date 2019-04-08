<template>
  <v-card flat tile>
    <v-img :src="`./assets/${pokemon.originalId}${pokemon.name}.png`" height="200px" width="200px"></v-img>
    <v-card-title primary-title>
      <div>
        <h3 class="headline mb-0">{{pokemon.name}}</h3>
        <ul>
            <li>{{pokemon.moves[0].name}}</li>
            <li>{{pokemon.moves[1].name}}</li>
            <li>{{pokemon.moves[2].name}}</li>
            <li>{{pokemon.moves[3].name}}</li>
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
