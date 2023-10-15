<template>
  <div id="app">
    <!-- <h2>{{artist.data.artists[0].name }}</h2>
    <h2>{{ artist.data.year.toString() | obfuscate}}</h2>
    <ul>
      <li v-for="genre in artist.data.genres" :key="genre">{{ genre }}</li>
    </ul>
    <ol class=""><li v-for="track in artist.data.tracklist" :key="track">{{ track.title  }}</li></ol> -->

    <h2>{{ artist.data.name }}</h2>
    <h3 v-for="release in releases" :key="release">{{ release.title }}</h3>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'App',
  data() {
    return {
      artist: null,
      id: "23755",
      jazzArtists: [
        23755,
        61585,
        252310,
        97545,
      ],
      releases: [],
      result: null,
    }
  },
  components: {

  },
  mounted () {
    // axios.get("https://api.discogs.com/masters/" + this.id).then((res) =>{
    //   this.artist = res
    // })
    axios.get("https://api.discogs.com/artists/" + this.id + "?per_page=100" ).then((res) =>{
      this.artist = res
      axios.get(this.artist.data.releases_url).then(res => this.releases = res.data.releases)
    })
    axios.get()
  },
  filters: {
    obfuscate: function(value) {
      return value.replace(/[^ ]/g, 'x');
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
