<template>
  <div id="app">
    <h1 class="title">PlatziMusic</h1>
    <select v-model="selectedCountry" class="select">
      <option v-for="country in countries" :value="country.value">{{ country.name }}</option>
    </select>
    <spinner v-show="loading"></spinner>
    <ul>
      <artist v-for="artist in artists" :artist="artist" :key="artist.mbid"></artist>
    </ul>
  </div>
</template>

<script>
import Artist from './components/Artist.vue'
import Spinner from './components/Spinner.vue'
import getArtists from './api'

export default {
  name: 'app',
  data () {
    return {
      artists: [],
      countries: [
        { name: 'México', value:'mexico'},
        { name: 'Colombia', value:'colombia'},
        { name: 'Argentina', value:'argentina'},
        { name: 'España', value:'spain'}
      ],
      selectedCountry: 'mexico',
      loading: true
    }
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtist() {
      this.loading = true
      const self = this
      this.artists = []
      getArtists(this.selectedCountry)
      .then(function (artists) {
        self.loading = false
        self.artists = artists
      })
    }
  },
  mounted() {
    this.refreshArtist()
  },
  watch: {
    selectedCountry() {
      this.refreshArtist()
    }
  }
}
</script>

<style lang="stylus">
#app
 font-family 'Avenir', Helvetica, Arial, sans-serif
 -webkit-font-smoothing antialiased
 -moz-osx-font-smoothing grayscale
 text-align center
 color #2c3e50

h1, h2
 font-weight normal

ul
 list-style-type none
 padding 0

li
 display inline-block
 margin 0 10px

a
 color #42b983

h1.title
  color #41b883
  background-color #35495e
  padding 20px
  font-size 45px

.select
  color #41b883
  background-color #FFFFFF
  border-radius 10px
  font-size 25px
  padding 5px 20px
</style>
