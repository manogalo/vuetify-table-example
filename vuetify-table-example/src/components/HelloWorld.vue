<template>
  <v-container>
      <v-data-table
        :items="chars"
        item-key="name"
        :loading="loading"
        loading-text="Carregando tabela"
      ></v-data-table>
  </v-container>
</template>

<script>
  import axios from 'axios'

  export default {
    data() {
      return {
        chars: [],
        loading: true
      }
    },
    mounted() {
      axios.get('https://swapi.dev/api/people/')
        .then(response => {
          this.chars = response.data.results
          this.loading = false
        }) 
    }
  }
</script>
