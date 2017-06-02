<template>
  <div class="container">
    <Affix/>
    <div class="home-content">

      <h1>{{msg}}</h1>
      <button @click="getCollections" type="button" name="button">get collection</button>
      <button @click="getDocuments" type="button" name="button">get documents</button>

    </div>
</div>

</template>

<script>
import Affix from '~components/Affix.vue'
import axios from 'axios'
export default {
  data () {
    return {
      msg: 'votre plus beau profil',
      request: 'https://api.mlab.com/api/1/',
      apiKey: 'f-uDQagLij0gzft6G5473mVMsawV6Yy7'
    }
  },
  components: {
    Affix
  },
  methods: {
    getCollections: function () {
      axios.get('https://api.mlab.com/api/1/databases/fishblock/collections?apiKey=' + this.apiKey)
      .then(response => {
        // JSON responses are automatically parsed.
        console.log(response.data)
      })
      .catch(e => {
        this.errors.push(e)
      })
    },
    getDocuments: function () {
      axios.get('https://api.mlab.com/api/1/databases/fishblock/collections/Users?apiKey=' + this.apiKey)
      .then(response => {
        // JSON responses are automatically parsed.
        console.log(response.data)
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  }

}
</script>


<style lang="css" scoped>
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
