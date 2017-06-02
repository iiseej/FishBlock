<template>
  <div class="container">

    <Affix/>
    <div class="home-content">
    <searchBar/>
    <div id="space-top"></div>

    <!-- Photo and name -->
    <div class="profil-details">
      <img src="~assets/profilPicture.jpg" alt="Profil Picture" class="rounded-picture"/>
      <p id="profil-details-text">Update picture</p>
      <div id="profil-details-elements">
        <p id="profil-details-name">Klaus ,</p>
        <p id="profil-details-age">24</p>
        <img src="~assets/pen.png" alt="Update user informations" class="profil-details-update"/>
      </div>

      <button @click="getCollections" type="button" name="button">get collection</button>
      <button @click="getDocuments" type="button" name="button">get documents</button>

    </div>

    <!-- Recent activity -->
     <div class="profil-details-activity">
        <div class="profil-details-activity-title">
          <div id="profil-details-activity-text">
            <img src="~assets/lastEpisodes.png" id="profil-details-activity-icon"/> Recent activity
          </div>
        </div>
        <div class="profil-details-favorites-title">
          <div id="profil-details-favorites-text">
            Favorites tvshows <img src="~assets/critics.png" id="profil-details-favorites-icon"/>
          </div>
        </div>
      </div>

          <div class="profil-details-activity-content">
            <div class="profil-details-activity-element">

            </div>
          </div>

          <!-- Favorites tvshows -->
          <div class="profil-details-favorites-element">

            <div class="profil-details-favorites-gradient">
              <li v-for="movie in movies" class="profil-details-favorites-list">
                <div class="profil-details-favorites-one">
                  <img :src="img_path + movie.backdrop_path" class="profil-details-favorites-img"/>
                  <div class="home-last-tvshows-background"></div>
                  <nuxt-link :to="'/show/' + movie.id">
                    <p class="profil-details-favorites-name">{{movie.name}}</p>
                    <p class="profil-details-favorites-vote"><img src="~assets/heart.png" id="shows-posters-vote-img"/>{{movie.vote_average}}</p>
                  </nuxt-link>
                </div>
              </li>
            </div>

          </div>

    </div>

  </div>
</template>


<!-- Scripts -->
<script>
  import Affix from '~components/Affix.vue'
  import searchBar from '~components/searchBar.vue'
  import axios from 'axios'
  export default {
    data () {
      return {
        msg: 'votre plus beau profil',
        request: 'https://api.mlab.com/api/1/',
        apiKeyMongo: 'f-uDQagLij0gzft6G5473mVMsawV6Yy7',
        apiKeyTvdb: '028097eda8e5dd43094c8fcbaf15a506',
        img_path: 'https://image.tmdb.org/t/p/w780/',
        movies: [],
        errors: [],
        showsFollowed: []
      }
    },
    components: {
      Affix,
      searchBar
    },
    methods: {
      getCollections: function () {
        axios.get('https://api.mlab.com/api/1/databases/fishblock/collections?apiKey=' + this.apiKeyMongo)
        .then(response => {
          // JSON responses are automatically parsed.
          console.log(response.data)
        })
        .catch(e => {
          this.errors.push(e)
        })
      },
      getDocuments: function () {
        axios.get('https://api.mlab.com/api/1/databases/fishblock/collections/Users?apiKey=' + this.apiKeyMongo)
        .then(response => {
          // JSON responses are automatically parsed.
          console.log(response.data)
        })
        .catch(e => {
          this.errors.push(e)
        })
      }
    },
    // Fetches posts when the component is created.
    created () {
      axios({
        method: 'get',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users/59300f38f36d2805427e6df7?apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7'
      }).then(response => {
        if (response.data.length === 0) {
          console.log('show is not followed')
        } this.showsFollowed = response.data.followedTvShows
        this.showsFollowed = this.showsFollowed.splice(0, 3)
        console.log(this.showsFollowed[0])
        axios.get('https://api.themoviedb.org/3/tv/' + this.showsFollowed[0] + '?api_key=' + this.apiKeyTvdb + '&language=en-US')
        .then(response => {
          // JSON responses are automatically parsed.
          this.movies.push(response.data)
          // this.movies.push = response.data
        })
        .catch(e => {
          this.errors.push(e)
        })
        axios.get('https://api.themoviedb.org/3/tv/' + this.showsFollowed[1] + '?api_key=' + this.apiKeyTvdb + '&language=en-US')
        .then(response => {
          // JSON responses are automatically parsed.
          this.movies.push(response.data)
          // this.movies.push = response.data
        })
        .catch(e => {
          this.errors.push(e)
        })
        axios.get('https://api.themoviedb.org/3/tv/' + this.showsFollowed[2] + '?api_key=' + this.apiKeyTvdb + '&language=en-US')
        .then(response => {
          // JSON responses are automatically parsed.
          this.movies.push(response.data)
          // this.movies.push = response.data
        })
        .catch(e => {
          this.errors.push(e)
        })
      })
    }
  }
</script>


<!-- CSS in order of apparition -->
<style lang="css" scoped>
  #container {
    display: flex;
    min-height: 100vh;
  }

  .home-content {
    flex: 1 1 auto;
    background-color: #262835;
    height: auto;
    margin-left: 220px
  }

  #space-top {
    height: 50px;
  }

  .profil-details {
    width: 20%;
    min-width: 200px;
    margin-top: 30px;
    margin-left: 30px;
  }

  .rounded-picture {
    overflow: hidden;
    -webkit-border-radius: 200px;
    -moz-border-radius: 200px;
    border-radius: 200px;
    width: 200px;
    height: 200px;
    display: block;
    margin: auto;
    margin-bottom: 30px;
  }

  #profil-details-text {
    text-align: center;
    margin-top: -20px;
  }

  #profil-details-elements {
    text-align: center;
  }

  #profil-details-name {
    font-size: 24px;
    display: inline-block;
    margin-top: 20px;
  }

  #profil-details-age {
    font-weight: 400;
    display: inline-block;
    margin-left: 20px;
  }

  .profil-details-update {
    width: 10px;
    height: auto;
    margin-left: 10px;
  }

  .profil-details-activity {
    margin: 20px 20px 0px 20px;
    padding: 30px 35px 0px 30px;
    background-color: #161C28;
    z-index: -20;
    padding-bottom: 1px;
  }

  .profil-details-activity-title {
    width: 40%;
    padding-right: 10%;
  }

  #profil-details-activity-text {
    color: white;
    font-size: 12px;
    font-weight: 800;
    margin-top: -5px;
    margin-left: -15px;
    margin-bottom: 20px;
  }

  #profil-details-activity-icon {
    width: 10px;
    margin-right: 5px;
  }

  .profil-details-activity-content {
    width: 36%;
    height: 255px;
    display: inline-block;
    background-color: #161C28;
    vertical-align: top;
    margin-bottom: 30px;
  }

  .profil-details-activity-element {
    width: 92%;
    margin-right: 3%;
    height: 255px;
    display: inline-block;
    background-color: brown;
    vertical-align: top;
  }

  .profil-details-favorites-element {
    width: 64%;
    height: 255px;
    display: inline-block;
    overflow: hidden;
    position: relative;
    z-index: 100;
  }

  .profil-details-favorites-title {
    margin-top: -35px;
  }

  #profil-details-favorites-text {
    color: white;
    font-size: 12px;
    font-weight: 800;
    margin-top: -5px;
    margin-right: -15px;
    margin-bottom: 20px;
    text-align: right;
  }

  #profil-details-favorites-icon {
    width: 10px;
    margin-left: 5px;
  }

  .profil-details-favorites-gradient {
    background-image: -webkit-linear-gradient(bottom, rgba(0, 0, 0, 0.8) 0%, rgba(0, 0, 0, 0.2) 100%);
    position: relative;
    width: 100%;
    height: 255px;
  }

  .profil-details-favorites-list {
    list-style: none;
    margin: 0;
    padding: 0;
    width: 33.33%;
    display: inline-block;
    position: relative;
  }

  .profil-details-favorites-one {
    overflow: hidden;
    margin-top: -20px;
  }

  .profil-details-favorites-img {
    margin-left: -40%;
    height: 280px;
    position: relative;
    z-index: -10;
  }

  .profil-details-favorites-name {
    margin-top: -70px;
    margin-bottom: 60px;
    text-align: center;
  }

  .profil-details-favorites-vote {
    margin-top: -50px;
    margin-bottom: 50px;
    text-align: center;
    font-size: 12px;
    font-weight: 400;
    color: #ff9941
  }

  #shows-posters-vote-img {
    width: 8px;
    margin-right: 5px;
  }
</style>
