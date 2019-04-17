<template>
  <v-container fluid grid-list-sm>
    <v-layout row wrap>
      <v-flex v-for="pokemon in pokemons" :key="pokemon.originalId">
        <PokeCard :pokemon="pokemon"/>
      </v-flex>
    </v-layout>
    <div id="formContainer">
      <v-form ref="form" v-model="valid" lazy-validation>
        <v-text-field id="name" v-model="name" label="Name" required></v-text-field>
        <v-text-field id="url" v-model="url" label="URL" required></v-text-field>
        <v-text-field id="height" v-model="height" label="Height" required></v-text-field>
        <v-text-field id="weight" v-model="weight" label="Weight" required></v-text-field>
        <v-text-field id="move1" v-model="move1" label="Move #1" required></v-text-field>
        <v-text-field id="move2" v-model="move2" label="Move #2" required></v-text-field>
        <v-text-field id="move3" v-model="move3" label="Move #3" required></v-text-field>
        <v-text-field id="move4" v-model="move4" label="Move #4" required></v-text-field>
        <v-select :items="items" label="Type" v-model="selected"></v-select>
      </v-form>
      <v-btn color="info" @click="createPokemon">Create New Pokemon</v-btn>
    </div>
  </v-container>
</template>
<script>
import gql from "graphql-tag";
import PokeCard from "./PokeCard.vue";
// import POKEMON_CREATE from "../graphql/PokemonCreate.gql";

export default {
  components: {
    PokeCard
  },
  data() {
    return {
      items: ["Poison", "Fire", "Flying", "Grass", "Normal"],
      pokemons: [],
      valid: true,
      name: "",
      url: "",
      height: 0,
      weight: 0,
      move1: "",
      move2: "",
      move3: "",
      move4: "",
      selected: "Poison"
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
      // const name = this.name;
      // const url = this.url;
      // const weight = this.weight;
      // const height = this.height;
      // const move1 = this.move1;
      // const move2 = this.move2;
      // const move3 = this.move3;
      // const move4 = this.move4;
      try {
        this.$apollo
          .mutate({
            mutation: gql`
              mutation createPokemon(
                $name: String, $url: String, $weight: Int, $height: Int, $moves: MoveCreateManyInput) {
                createPokemon(data: {
                   name: $name,
                   url: $url,
                   weight: $weight,
                   height: $height,
                   moves: $moves,
                  
                   }
                   )
                   {
                  id
                  name
                  }
                }
            `,
            variables: {
              name: this.name,
              url: this.url,
              weight: this.weight,
              height: this.height,
              moves: {
                create: [
                  {name: this.move1}, 
                  {name: this.move2},
                  {name: this.move3},
                  {name: this.move4},
                ]
              },
              // types: {
              //   create: [
              //     { name: this.selected
              //     }
              //   ]
              // }
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
#formContainer {
  width: 500px;
  margin: auto;
}
</style>