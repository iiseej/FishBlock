<template>
  <div class="container">
    <Affix/>
    <div class="home-content">
      <h1>{{msg}}</h1>
    </div>
</div>

</template>

<script>
import Affix from '~components/Affix.vue'
export default {
  data () {
    return {
      msg: 'vos settings'
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
  margin-left: 220px
}
</style>
