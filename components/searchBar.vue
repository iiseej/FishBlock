<template lang="html">
  <div>
    <div :searchQuery="query" id="search-bar" @mouseleave="searchBarShow = false">
      <input @keyup="search(), searchResults = true" v-if="searchBarShow" type="text" name="" value="" v-model="query" placeholder="   Search tvshows" id="search-bar-input">
      <img @click="searchDone = true" @mouseover="searchBarShow = true" id="search-bar-img" src="~assets/searchIcon.png" alt="search button">
    </div>

    <!-- Results of search -->
    <div id="search-bar-results" v-if="searchResults" @mouseleave="searchResults = false">
      <li v-for="result in results" class="search-bar-results-element">
        <nuxt-link :to="'/show/' + result.id">
          <div class="search-bar-results-link">
            {{result.name}}
          </div>
        </nuxt-link>
      </li>
    </div>

  </div>
</template>


<!-- Scripts -->
<script>
  import axios from 'axios'
  export default {
    data: () => ({
      img_path: 'https://image.tmdb.org/t/p/w500/',
      apiKey: '028097eda8e5dd43094c8fcbaf15a506',
      results: [],
      query: '',
      searchBarShow: false,
      searchDone: false,
      searchResults: true
    }),
    methods: {
      search: function () {
        axios.get('https://api.themoviedb.org/3/search/tv?api_key=' + this.apiKey + '&language=en-US&query=' + this.query + '&page=1')
        .then(response => {
          // JSON responses are automatically parsed.
          this.results = response.data.results.splice(0, 5)
          console.log(this.results)
        })
        .catch(e => {
          this.errors.push(e)
        })
      }
    }
  }
</script>


<!-- CSS in order of apparition -->
<style lang="css">
  #search-bar {
    width: 100%;
    height: 50px;
    background-color: rgba(38, 40, 53, 0.6);
    position: fixed;
    z-index: 1000;
    top: 0px;
  }

  #search-bar-input {
    right: 280px;
    position: absolute;
    width: 180px;
    height: 20px;
    margin-top: 14px;
    border-radius: 15px;
    border-style: hidden;
    background-color: #e9e9e9;
    color: black;
  }

  #search-bar-img {
    height: 25px;
    width: auto;
    margin-top: 11px;
    right: 240px;
    position: absolute;
  }

  #search-bar-results {
    width: 180px;
    height: auto;
    position: fixed;
    right: 60px;
    top: 50px;
    background-color: #161C28;
    z-index: 1000;
  }

  .search-bar-results-element {
    list-style: none;
    margin: 0;
    padding: 0;
  }

  .search-bar-results-link {
    margin: 0;
    padding: 10px 30px 10px 30px;
  }

  .search-bar-results-link:hover {
    background-color: #ff9941;
    color: black;
  }
</style>
