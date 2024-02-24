<template>
  <v-container>
      <v-data-table
        :items="chars"
        :headers="headers"
        item-key="name"
        :loading="tableLoading"
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
        tableLoading: true,
        headers: [
          { title: 'Nome', value: 'name' }
        ]
      }
    },
    mounted() {
      axios.get('https://swapi.dev/api/people/')
        .then(response => {
          this.chars = response.data.results
          this.tableLoading = false
        }) 
    }
  }
</script>
