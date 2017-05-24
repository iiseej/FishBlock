<template>
  <div class="container">
    <Affix/>
    <div class="home-content">
      <Searchbar/>
      <h1>{{msg}}</h1>
      <div id="wrapper">
    <div style="position: absolute; left: 10px; top: 10px; width:200px; height:100px; background-color: yellow;">
        abcd
    </div>
    <div style="position: absolute; z-index: 1; left: 50px; top: 20px; width:100px; height:20px; background-color: green;">
        1234
    </div>
</div>
    </div>
  </div>

</template>

<script>
import Affix from '~components/Affix.vue'

export default {
  data () {
    return {
      msg: 'this is your home'
    }
  },
  components: {
    Affix
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
