<template lang="html">
  <div id="search">
  <!-- <input type="text" name="search shows .." value="" v-on:click="show = !show"> -->
  <img src="~assets/SearchIcon.png" v-on:click="show = !show">
  <transition name="fade" mode="out-in">
    <input v-if="show" class="input_search" type="text" value="search shows ...">
  </transition>
</div>
</template>

<script>
export default {
  data () {
    return {
      show: true
    }
  }
}
</script>

<style lang="css">
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s
}
.fade-enter, .fade-leave-to /* .fade-leave-active in <2.1.8 */ {
  opacity: 0
}

.input_search {
  position: absolute;
  border: none;
  outline: none;
  background: #161C28;
  width: auto;
  height: 35px;
  margin: 0;
  z-index: 10;
  padding: 0px 65px 20px 20px;
  font-family: inherit;
  font-size: 20px;
  color: #2c3e50;
  padding-top: 1%;
  margin-left: 1%;

}

#search img {
  height: 32px;
  width: auto;
}

#search {
  width: auto;
  padding-top: 1%;
  padding-left: 68%;
}

</style>
