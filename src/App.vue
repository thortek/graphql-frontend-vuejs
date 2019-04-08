<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Pokemon</span>
        <span class="font-weight-light">Data Viewer</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn
        flat
        href="https://github.com/thortek"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <PokeList/>
    </v-content>
  </v-app>
</template>

<script>
import PokeList from './components/PokeList'

export default {
  name: 'App',
  components: {
    PokeList
  },
  data () {
    return {
      //
    }
  }
}
</script>
