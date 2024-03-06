<template>
  <v-container>
    <v-data-table
      :items="chars"
      :headers="headers"
      item-key="name"
      :loading="tableLoading"
      loading-text="Carregando tabela"
    >
      <template v-slot:top>
        <v-toolbar flat>
          <v-toolbar-title>Star Wars Characters</v-toolbar-title>
          <v-divider class="mx-4" inset vertical />
          <v-spacer />
            <v-btn color="success" v-bind="props" @click="getWeatherForecast">
              <v-icon icon="mdi-file-excel-outline" color="success"></v-icon>
              Download
            </v-btn>
        </v-toolbar>
      </template>
    </v-data-table>
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
          { title: 'Nome', value: 'name' },
          { title: 'Altura (cm)', value: 'height' },
          { title: 'Peso (kg)', value: 'mass' },
          { title: 'Cor do cabelo', value: 'hair_color' },
          { title: 'Cor da pele', value: 'skin_color' },
          { title: 'Cor dos olhos', value: 'eye_color' },
          { title: 'Gênero', value: 'gender' }
        ]
      }
    },
    mounted() {
      axios.get('https://swapi.dev/api/people/')
        .then(response => {
          this.chars = response.data.results
          this.tableLoading = false
        }) 
    },
    methods: {
      testeBotaoDownload() {
        alert('Opa')
      },
      getWeatherForecast() {
        axios.get('https://localhost:7041/WeatherForecast/')
          .then(response => console.log(response.data))
      }
    }
  }
</script>
