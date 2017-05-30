<template>
  <div class="container">
    <Affix/>
    <div class="home-content">
      <h1>{{msg}}</h1><Dropdown/>
      <div class="dropdown">
        <button class="btn dropdown-toggle sr-only" type="button" id="" data-toggle="dropdown">

          <span class="caret"></span>
        </button>
        <ul class="dropdown-menu" role="menu" aria-labelledby="">

        </ul>
      </div>
    </div>
  </div>

</template>

<script>
import Affix from '~components/Affix.vue'
import Dropdown from '~components/Dropdown.vue'

export default {
  data () {
    return {
      msg: 'this is your home'
    }
  },
  components: {
    Affix,
    Dropdown
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
