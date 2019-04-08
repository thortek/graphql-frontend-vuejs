<template>
  <v-container fluid grid-list-sm>
    <v-layout row wrap>
      <v-flex v-for="pokemon in pokemons" :key="pokemon.originalId">
        <PokeCard :pokemon="pokemon"/>
        <!-- <PokeCard v-for="pokemon in pokemons"
            :key="pokemon.originalId"
        :pokemon="pokemon"/>-->
        <!-- <v-card flat tile>
                <v-img
                  :src="`https://unsplash.it/150/300?image=${Math.floor(Math.random() * 100) + 1}`"
                  height="200px"
                ></v-img>
        </v-card>-->
      </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
import gql from "graphql-tag";
import PokeCard from "./PokeCard.vue";

export default {
  components: {
    PokeCard
  },
  data() {
    return {
      info: "",
      pokemons: []
    };
  },
  mounted() {
    // return axios
    //   .get("https://pokeapi.co/api/v2/pokemon/1")
    //   .then(response => (this.info = response));
  },
  apollo: {
    pokemons: gql`
      query {
        pokemons {
          originalId
          name
          weight
          height
          moves {
            name
            url
          }
          types {
            name
          }
        }
      }
    `
  }
};
</script>
<style>
</style>