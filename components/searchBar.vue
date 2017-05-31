<template lang="html">
  <div>



  <div  :searchQuery="query" class="search">
    <input @keyup="search" v-if="searchBarShow" type="text" name="" value="" v-model="query" placeholder="search shows or people">
    <img @click="searchDone = true" @mouseover="searchBarShow = true"style="height:30px;width:auto;" src="~assets/searchIcon.png" alt="">
  </div>


  <!-- Results of search -->


  <!-- Results of search -->

  <div id="resultsOfSearch">
    <li v-for="result in results" ><nuxt-link :to="'/show/' + result.id"><div style="height:5Opx;width:auto;">
      {{result.name}}
    </div></nuxt-link></li>
  </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data: () => ({
    img_path: 'https://image.tmdb.org/t/p/w500/',
    apiKey: '028097eda8e5dd43094c8fcbaf15a506',
    results: [],
    query: '',
    searchBarShow: false,
    searchDone: false
  }),
  methods: {
    search: function () {
      axios.get('https://api.themoviedb.org/3/search/tv?api_key=' + this.apiKey + '&language=en-US&query=' + this.query + '&page=1')
      .then(response => {
        // JSON responses are automatically parsed.
        this.results = response.data.results
        console.log(this.results)
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }
}
</script>

<style lang="css">
</style>
