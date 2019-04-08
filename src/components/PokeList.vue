<template>
  <v-container fluid grid-list-sm>
    <v-layout row wrap>
            <v-flex
              v-for="n in 9"
              :key="n"
              xs4
            >
              <v-card flat tile>
                <v-img
                  :src="`https://unsplash.it/150/300?image=${Math.floor(Math.random() * 100) + 1}`"
                  height="200px"
                ></v-img>
              </v-card>
            </v-flex>
    </v-layout>
  </v-container>
</template>
<script>
import axios from 'axios'
import gql from 'graphql-tag'

export default {
  data() {
    return {
      info: "",
      pokemon: []
    };
  },
  mounted() {
    // return axios
    //   .get("https://pokeapi.co/api/v2/pokemon/1")
    //   .then(response => (this.info = response));
  },
  apollo: {
    pokemons: gql`query {
      pokemons {
        name
      }
    }`,
  }
};
</script>
<style>
</style>