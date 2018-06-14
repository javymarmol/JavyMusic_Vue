<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>JavyMusic</h1>
    <select v-model="selectedCountry">
      <option v-for="country in countries" :value="country.name">{{ country.name}}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <Artist v-for="artist in artists" v-bind:artist="artist" v-bind:key="artist.mbid">
      </Artist>
    </ul>
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import {getArtists, getContries} from './api'
import Spinner from "./components/Spinner";
export default {
  name: 'app',
  data () {
    return {
      artists: [],
      /*countries:[
        { name: 'Argentina', value: 'argentina'},
        { name: 'Colombia', value: 'colombia'},
        { name: 'España', value: 'spain'}
      ],*/
      countries: [],
      selectedCountry: 'Colombia',
      loading: true
    }
  },
  components: {
    Spinner,
    Artist
  },
  methods: {
    refreshArtists(){
      const self = this
      this.loading = true
      this.artists = []
      getArtists(this.selectedCountry)
        .then( function (artists) {
          self.loading = false
          self.artists = artists
        })
    },
    loadCountries(){
      const self = this
      getContries()
        .then( function (countries) {
          self.countries = countries
          console.log(countries)
        })
    }
  },
  mounted: function () {
    this.loadCountries()
    this.refreshArtists()
  },
  watch: {
    selectedCountry(){
      this.refreshArtists()
    }
  }
}
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
