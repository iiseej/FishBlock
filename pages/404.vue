<template lang="html">
  <div class="container">
    <Affix/>
    <div id="content">
      <img src="~assets/klausZombie.png" alt="klaus zombie" id="klaus-img">
      <h1>404 : page not found !</h1>
      <h2>Bring me back in my Popcorn fish bowl :)</h2>
    </div>
  </div>
</template>


<!-- Scripts -->
<script>
  import Affix from '~components/Affix.vue'
  export default {
    components: {
      Affix
    }
  }
</script>


<!-- CSS in order of apparition -->
<style lang="css">
  body {
    background-color: #262835;
  }
  
  .container {
    height: auto;
  }

  #content {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    height: auto;
    margin-left: 220px; 
  }
  
  #klaus-img {
    margin-top: 10%;
    width: 400px;
    margin-bottom: 30px;
  }

  h1 {
    color: #ff9941;
  } 
  
  h2 {
    color: #ff9941;
    font-weight: 400;
    font-size: 14px;
  }
</style>
