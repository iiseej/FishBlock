
<template>
  <div class="container">
    <Affix/>
  <div class="content">
    <p><strong>{{movie.original_title}}</strong></p>
    <img :src="'https://image.tmdb.org/t/p/w500/'+movie.poster_path" alt="">
  </div>
</div>
</template>

<script>
import axios from 'axios'
import Affix from '~components/Affix.vue'

export default {
  data: () => ({
    movie: {},
    errors: []
  }),
  components: {
    Affix
  },

  // Fetches posts when the component is created.
  created () {
    console.log(this.$route.params.id)
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '?api_key=028097eda8e5dd43094c8fcbaf15a506&language=en-US')
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
<style media="screen">
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
