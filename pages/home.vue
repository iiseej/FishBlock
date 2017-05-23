<template>
  <div class="container">
    <Affix/>
    <div class="home-content">
      <Searchbar/>
      <h1>{{msg}}</h1>
    </div>
  </div>

</template>

<script>
import Affix from '~components/Affix.vue'
import Searchbar from '~components/Searchbar.vue'
export default {
  data () {
    return {
      msg: 'this is your home'
    }
  },
  components: {
    Affix,
    Searchbar
  }

}
</script>


<style lang="css">
#container {
  display: flex;
  min-height: 100vh;
}
.home-content {
  flex: 1 1 auto;
  background-color: #262835;
  height: 2000px;
  margin-left: 220px;
}

.search {
  display: inline-block;
}
</style>
