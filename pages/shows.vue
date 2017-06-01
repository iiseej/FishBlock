
<template>
  <div class="container">
    <Affix/>
    <div class="content">



      <!-- Alphabetical list of tvshows -->

      <searchBar/>
      <div id="space-top"></div>

      <!-- Alphabetical list of tvshows -->
      <button @click="prevPage"type="button" name="button">previous page</button>
      <button @click="nextPage"type="button" name="button">next page</button>

      <div class="shows-list-content" >
        <p v-for="letter in alphabet" id="shows-list-text" >{{letter}}</p>
      </div>

      <!-- Posters of tvshows -->
      <div class="shows-posters-content">
        <ul>
          <li v-for="movie in movies" id="shows-posters-list">
            <nuxt-link :to="'/show/' + movie.id">
              <div>
               <p id="shows-posters-title">{{movie.original_name}}</p>
               <p id="shows-posters-genre">{{movie.vote_average}}</p>
                <img  id="shows-posters-img" :src="'https://image.tmdb.org/t/p/w500/'+movie.poster_path" alt="">
              </div>
            </nuxt-link>
          </li>
        </ul>
      </div>
  </div>
</div>
</template>


<!-- Scripts -->
<script>
import axios from 'axios'
import Affix from '~components/Affix.vue'
import searchBar from '~components/searchBar.vue'

export default {
  data: () => ({
    apiKey: '028097eda8e5dd43094c8fcbaf15a506',
    movies: [],
    errors: [],
    alphabet: ['0-9', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z'],
    page: 1
  }),
  methods: {
    nextPage: function () {
      this.page = this.page + 1
      axios.get('https://api.themoviedb.org/3/discover/tv?api_key=' + this.apiKey + '&language=en-US&sort_by=popularity.desc&page=' + this.page + '&timezone=America%2FNew_York&vote_average.gte=7&include_null_first_air_dates=false')
      .then(response => {
        // JSON responses are automatically parsed.
        // this.movie = response.data
        console.log(response.data.results[0])
        this.movies = response.data.results
        // this.movies.name_original = response.data.original_name.substring(0, 22)
      })
      .catch(e => {
        this.errors.push(e)
      })
    },
    prevPage: function () {
      if (this.page === 1) {
        return
      } else {
        this.page = this.page - 1
        axios.get('https://api.themoviedb.org/3/discover/tv?api_key=' + this.apiKey + '&language=en-US&sort_by=popularity.desc&page=' + this.page + '&timezone=America%2FNew_York&vote_average.gte=7&include_null_first_air_dates=false')
        .then(response => {
          // JSON responses are automatically parsed.
          // this.movie = response.data
          console.log(response.data.results[0])
          this.movies = response.data.results
          // this.movies.name_original = response.data.original_name.substring(0, 22)
        })
        .catch(e => {
          this.errors.push(e)
        })
      }
    }
  },
  components: {
    Affix,
    searchBar
  },
  // Fetches posts when the component is created.
  created () {
    axios.get('https://api.themoviedb.org/3/discover/tv?api_key=' + this.apiKey + '&language=en-US&sort_by=popularity.desc&page=' + this.page + '&timezone=America%2FNew_York&vote_average.gte=7&include_null_first_air_dates=false')
    .then(response => {
      // JSON responses are automatically parsed.
      // this.movie = response.data
      console.log(response.data.results[0])
      this.movies = response.data.results
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>


<!-- CSS in order of apparition -->
<style media="screen" scoped>
  ul{
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
    flex-direction: row;
    align-items: center;
  }
  #container {
    min-height: 100vh;
  }
  .content {
    background-color: #262835;
    height: auto;
    margin-left: 220px;
    justify-content: center;
  }

  #space-top {
    height: 60px;
  }

  .shows-list-content {
    width: 100%;
    display: flex;
    justify-content: space-around;
    text-align: center;
    margin-top: 50px;
  }

  .shows-posters-content {
    display: block;
  }

  #shows-list-text {
    font-size: 20px;

  }
  #shows-list-text:hover {
    -moz-transform: scale(1.5);
    -webkit-transform: scale(1.5);
    transform: scale(1.5);
    color: #ff9941;

  }

  #shows-posters-list {
    margin: 0;
    padding: 20px;
  }

  #shows-posters-title[data-v-48e3a7d3] {
    position: absolute;
    margin-top: 212px;
    padding: 10px 0;
    font-size: 16px;
    background-color: rgba(0, 0, 0, 0.6);
    width: 180px;
    height: 58px;
    text-align: center;
  }

  #shows-posters-title[data-v-48e3a7d3]:hover {
    background-color: #ff9941;
    color: black;
    font-weight: 800;
  }

  #shows-posters-genre {
    position: absolute;
    margin-top: 248px;
    font-size: 11px;
    width: 180px;
    text-align: center;
  }

  #shows-posters-img {
    height: auto;
    width:180px;
  }

    ::-webkit-scrollbar {
      width: 12px;
  }

  ::-webkit-scrollbar-track {
      background: #161C28;
  }

  ::-webkit-scrollbar-thumb {
    background: #e8e8e8;
    -webkit-border-radius: 10px;
    border-radius: 10px;
  }
</style>
