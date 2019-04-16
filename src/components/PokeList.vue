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

    <v-form ref="form" v-model="valid" lazy-validation>
      <v-text-field id="name" v-model="name" label="Name" required></v-text-field>

      <v-text-field id="url" v-model="url" label="URL" required></v-text-field>
    </v-form>

    <v-btn color="info" @click="createPokemon">Create New Pokemon</v-btn>
  </v-container>
</template>
<script>
import gql from "graphql-tag";
import PokeCard from "./PokeCard.vue";
import POKEMON_CREATE from "../graphql/PokemonCreate.gql";

export default {
  components: {
    PokeCard
  },
  data() {
    return {
      info: "",
      pokemons: [],
      valid: true,
      name: "",
      url: ""
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
  },
  methods: {
    createPokemon() {
      const name = this.name;
      const url = this.url;
      try {
        this.$apollo
          .mutate({
            mutation: gql`
              mutation createPokemon($name: String, $url: String) {
                createPokemon(data: { name: $name, url: $url }) {
                  id
                  name
                  url
                }
              }
            `,
            variables: {
              name,
              url
            }
          })
          .then(data => {
            console.log(data);
          });
      } catch (e) {
        console.error(e);
      }
    }
  }
};
</script>
<style scoped>
</style>