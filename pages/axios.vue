<template>
  <div class="">

        <p><strong>{{movie.original_title}}</strong></p>
        <img :src="'https://image.tmdb.org/t/p/w500/'+movie.poster_path" alt="">
    </ul>

    <ul v-if="errors && errors.length">
      <li v-for="error of errors">
        {{error.message}}
      </li>
    </ul>
  </div>

</template>

<script>
import axios from 'axios'

export default {
  data: () => ({
    movie: {},
    errors: []
  }),

  // Fetches posts when the component is created.
  created () {
    axios.get('https://api.themoviedb.org/3/movie/?api_key=028097eda8e5dd43094c8fcbaf15a506')
    .then(response => {
      // JSON responses are automatically parsed.
      this.movie = response.data
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
