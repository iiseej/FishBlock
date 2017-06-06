<template lang="html">
    <select>
      <h2>blabla</h2>
      <option v-for="item in series">{{ item.name }}</option>
    </select>
</template>

<script>
import axios from 'axios'
export default {
  data: () => ({
    series: []
  }),

  created () {
    axios.get('https://api.themoviedb.org/3/discover/tv?api_key=028097eda8e5dd43094c8fcbaf15a506&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1')
    .then(response => {
      console.log(response.data.results[0])
      this.series = response.data.results
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
}
</script>

<style lang="css">
#app {
  margin-left: 50%
}
</style>
