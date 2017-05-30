
<template>
  <div class="container">
    <Affix/>
  <div class="content">
    <ul>
      <li v-for="movie in movies"><nuxt-link :to="'/show/' + movie.id"><img style="height:400px;width:auto;" :src="'https://image.tmdb.org/t/p/w500/'+movie.poster_path" alt=""></nuxt-link></li>

    </ul>
  </div>
</div>
</template>

<script>
import axios from 'axios'
import Affix from '~components/Affix.vue'

export default {
  data: () => ({
    movies: [],
    errors: []
  }),
  components: {
    Affix
  },

  // Fetches posts when the component is created.
  created () {
    axios.get('https://api.themoviedb.org/3/discover/tv?api_key=028097eda8e5dd43094c8fcbaf15a506&language=en-US&sort_by=popularity.desc&page=1&timezone=America%2FNew_York&vote_average.gte=7&include_null_first_air_dates=false')
    .then(response => {
      // JSON responses are automatically parsed.
      // this.movie = response.data
      console.log(response.data.results[0])
      this.movies = response.data.results
    })
    .catch(e => {
      this.errors.push(e)
    })
    axios.get('https://api.themoviedb.org/3/discover/tv?api_key=028097eda8e5dd43094c8fcbaf15a506&language=en-US&sort_by=popularity.desc&page=2&timezone=America%2FNew_York&vote_average.gte=7&include_null_first_air_dates=false')
    .then(response => {
      // JSON responses are automatically parsed.
      // this.movie = response.data
      console.log(response.data.results[0])
      this.movies = response.data.results
    })
    .catch(e => {
      this.errors.push(e)
    })

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
  }
}
</script>
<style media="screen" scoped>
ul{
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  flex-direction: row;
  align-items: center;
}
#container {
  display: flex;
  min-height: 100vh;
}
.content {
  display:flex;
  flex: 1 1 auto;
  background-color: #262835;
  height: 2000px;
  margin-left: 220px;
  justify-content: center;
}
</style>
