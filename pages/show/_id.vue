
<template>
  <div class="container">
    <Affix/>
    <div class="content">

      <!-- Top banner of the tvshow --> 
      <div class="backdrop-gradient">
        <div class="backdrop">
          <img id="tvshow-backdrop" :src="'https://image.tmdb.org/t/p/original/'+movie.backdrop_path" alt="banner">
          <div class="tvshow-title">
            <p id="tvshow-title-text"><strong>{{movie.original_name}}</strong></p>
            <p id="tvshow-first-air-date"><strong>{{movie.first_air_date}}</strong></p>
            <p id="tvshow-genres-text"><strong><li class="tvshow-genres" v-for="genre in movie.genres"> {{genre.name}}</li></strong></p>
            <p id="tvshow-number-seasons">{{movie.number_of_seasons}} seasons</p>
            <p id="tvshow-last-air-date">Last episode aired {{movie.last_air_date}}</p>
            <div>
              <a href="route"><img src="~assets/FollowButton.png" id="tvshow-follow-btn"/></a>
            </div>
          </div>
        </div>
      </div>

      <!-- Details of tvshow and cast --> 
      <div class="tvshow-synopsis-cast">
        <div class="tvshow-synopsis">
          <div id="tvshow-about-text">
            <img src="~assets/about.png" id="tvshow-about-icon"/> About the show
          </div>
          <p id="tvshow-followers">254 Followers</p>
          <p id="tvshow-critics">26 Critics</p>
          <p v-if="seen" class="text-light" >{{overview}}</p>
        </div>
        <div class="tvshow-cast">
          <div id="tvshow-cast-text">
            The cast <img src="~assets/cast.png" id="tvshow-cast-icon"/>
          </div>
          <div @click="seen = !seen" id="tvshow-actor-photo-container">
            <li v-for="actor in cast" class="tvshow-actor-photo"><img id="tvshow-cast-poster" :src="'https://image.tmdb.org/t/p/original/'+actor.profile_path"/></li>
            <div>
              <li v-for="actor in cast" class="tvshow-actor-name">{{actor.name}}</li>
            </div>
          </div>
        </div>
      </div>

      <!-- Details of episodes and seasons --> 
      <div class="seasons-gradient">
        <div class="tvshow-seasons-episodes">
          <ul>
            <li id="tvshow-season-list" v-for="i in movie.number_of_seasons">
              <div class="tvshow-season-img"><p id="tvshow-season-text">season {{i}} {{seasonEpisodes.length}} episodes</p><img :src="'https://image.tmdb.org/t/p/original/' + season.poster_path" id="tvshow-season-poster"/></div>
              <ul>
                <div id="tvshow-episode-list">
                  <li v-for="episode in seasonEpisodes" class="tvshow-episode-number"><p>0</p></li>
                </div>
              </ul>
            </li>
          </ul>
        </div>
      </div>
      <div class="tvshow-episode-details">
      <ul>
        <li v-for="episode in seasonEpisodes" class="tvshow-episode-content">
          <div id="tvshow-episode-img">
            <a href="route"><img src="~assets/SawButton.png" id="tvshow-saw-btn"/></a>
            <img id="tvshow-episode-poster" :src="'https://image.tmdb.org/t/p/original/' + episode.still_path"/> 
          </div>
          <div id="tvshow-episode-text">
            <p id="tvshow-episode-title">{{episode.name}}</p>
            <p id="tvshow-episode-air-date">Release date {{episode.air_date}}</p>
            <p id="tvshow-episode-run-time">{{movie.episode_run_time[0]}} min</p>
            <p id="tvshow-episode-overview">{{episode.overview}}</p>
          </div>
        </li>
      </ul>
      </div>

    </div>
  </div>
</template>


<!-- Scripts --> 
<script>
import axios from 'axios'
import Affix from '~components/Affix.vue'

export default {
  data: () => ({
    apiKey: '028097eda8e5dd43094c8fcbaf15a506',
    movie: {},
    errors: [],
    cast: [],
    seen: true,
    overview: '',
    seasonEpisodes: [],
    season: {}
  }),
  components: {
    Affix
  },

  // Fetches posts when the component is created.
  created () {
    // datas of the global tvshow
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '?api_key=' + this.apiKey + '&language=en-US')
    .then(response => {
      // JSON responses are automatically parsed.
      this.movie = response.data
      this.movie.first_air_date = response.data.first_air_date.substring(0, 4)
      this.overview = response.data.overview
    })
    .catch(e => {
      this.errors.push(e)
    })
    // datas of the credits tvshow
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/credits?api_key=' + this.apiKey + '&language=en-US')
    .then(response => {
      // JSON responses are automatically parsed.
      this.cast = response.data.cast
    })
    .catch(e => {
      this.errors.push(e)
    })
    // datas of the tvshow seasons
    // for i=1  to this.seasons
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/season/3?api_key=' + this.apiKey + '&language=en-US')
    .then(response => {
      // JSON responses are automatically parsed.
      this.seasonEpisodes = response.data.episodes
      this.season = response.data
      console.log(this.seasonEpisodes)
      console.log(this.season)
    })
    .catch(e => {
      this.errors.push(e)
    })
    // apikey
    axios.get('https://api.themoviedb.org/3/person/122616?api_key=' + this.apiKey + '&language=en-U')
    .then(response => {
      // JSON responses are automatically parsed.
      console.log(this.cast[0].id)
    })
    .catch(e => {
      this.errors.push(e)
    })
  }
    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }

    // async / await version (created() becomes async created())
    //
    // try {
    //   const response = await axios.get(`http://jsonplaceholder.typicode.com/posts`)
    //   this.posts = response.data
    // } catch (e) {
    //   this.errors.push(e)
    // }
}
</script>

<!-- CSS in order of apparition --> 
<style media="screen">
  .container {
    display: flex;
    min-height: 100vh;
  }

  .content {
    padding-top: 60px;
    flex: 1 1 auto;
    z-index: 0;
    background-color: #262835;
    height: auto;
    margin-left: 220px;
    justify-content: center;
    position: relative;
  }

  .backdrop-gradient {
    background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.8) 0%, rgba(255, 255, 255, 0) 100%);
    position: relative;
  }  

  .backdrop {
    width: 100%;
    height: 200px;
    overflow: hidden;
    position: relative;
  }

  #tvshow-backdrop {
    width:100%; 
    position: relative;
    top: -50px; 
    z-index: -10;
  }

  .tvshow-title {
    z-index: 100;
    position: absolute;
    top: 10px;
    width: 100%;
  }

  #tvshow-title-text {
    font-size: 50px; 
    margin-left: 25px;
  }

  #tvshow-first-air-date {
    font-size: 20px; 
    margin-left: 25px;
  }

  #tvshow-genres-text {
    font-size: 14px; 
    margin-top: -24px; 
    margin-left: 70px;
  }

  .tvshow-genres {
    display: inline-block;
    padding-left: 20px;
  }  

  #tvshow-number-seasons {
    font-size: 14px; 
    margin-left: 25px; 
    margin-top: 45px;
  }

  #tvshow-last-air-date {
    font-size: 14px; 
    margin-left: 25px; 
    color: #ff9941;
  }

  #tvshow-follow-btn {
    width:130px; 
    height: auto; 
    margin-top: -32px; 
    position: absolute; 
    right: 30px;
  }

  .tvshow-synopsis-cast {
    margin: 20px;
    padding: 30px 35px;
    background-color: #161C28;
  }

  .tvshow-synopsis {
    width: 40%;
    padding-right: 10%;
    display: inline-block;
  }

  #tvshow-about-text {
    color: white;
    font-size: 12px;
    font-weight: 800;
    margin-top: -5px;
    margin-left: -15px;
    margin-bottom: 20px;
  }

  #tvshow-about-icon {
    width: 8px; 
    margin-right: 5px;
  }

  #tvshow-followers {
    font-size: 20px;
  }

  #tvshow-critics {
    font-size: 20px; 
    margin-bottom: 20px;
  }

  .text-light {
    font-weight: 400;
  }

  .tvshow-cast {
    display: inline-block;
    width: 60%;
    padding-left: 20px;
    vertical-align: top;
  }  

  #tvshow-cast-text {
    color: white;
    font-size: 12px;
    font-weight: 800;
    margin-top: -5px;
    margin-right: -15px;
    margin-bottom: 20px;
    text-align: right;
  }

  #tvshow-cast-icon {
    width: 10px;
    margin-left: 5px;
  }

  #tvshow-actor-photo-container {
    overflow-x: scroll;
    white-space: nowrap;
    max-width: 800px;
    margin-right: 0px;
  }  

  .tvshow-actor-photo {
    display: inline-block;
    padding-left: 0px;
  }  

  #tvshow-cast-poster {
    width: 130px; 
    height: auto;
  }

  .tvshow-actor-name {
    display: inline-block;
    padding-left: 0px;
    color: white;
    margin-bottom: 10px;
    font-size: 11px;
    width: 130px; 
    text-align: center;
  }

  ::-webkit-scrollbar {
      width: 12px;
  }

  ::-webkit-scrollbar-track {
      background: #161C28;
  }

  ::-webkit-scrollbar-thumb {
    background: #e8e8e8;
    -webkit-border-radius: 10px;
    border-radius: 10px;
  }

  .seasons-gradient {
    width: 35%;
    background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.8) 0%, rgba(255, 255, 255, 0) 100%);
    position: relative;
    display: inline-block;
    vertical-align: top;
  }  

  .tvshow-seasons-episodes {
    width: 100%;
  }  

  #tvshow-season-list {
    margin: 0;
    padding: 0px 0;
  }

  .tvshow-season-img {
    height: 50px;
    overflow: hidden;
    position: relative;
  }

  #tvshow-season-text {
    position: relative;
    top: 30%;
    vertical-align: middle;
    text-align: center;
    z-index: 100;
    font-size: 16px;
  }

  #tvshow-season-poster {
    width: 100%;
    margin-top: -200px;
    z-index: -10;
    position: relative;
  }  
  
  #tvshow-episode-list {
    width: 100%;
    background-color: #262835;
  }
  
  .tvshow-episode-number {
    width: 20%;
    display: inline-block;
    background-color: #4A4C55;
    text-align: center;
    padding: 20px;
  }
  
  .tvshow-episode-number:hover {
    background-color: #ff9941;
  }

  .tvshow-episode-details {
    width: 65%;
    display: inline-block;
  }

  .tvshow-episode-content {
    margin: 0;
    padding: 0;
  }

  #tvshow-episode-img {
    width: auto;
    height: 300px;
    overflow: hidden;
  }
  
  #tvshow-saw-btn {
    width:130px; 
    height: auto; 
    margin-top: 250px;
    position: absolute; 
    right: 30px;
  }

  #tvshow-episode-poster {
    width: 100%; 
    height: auto;
  }

  #tvshow-episode-text {
    padding: 20px 30px;
  }

  #tvshow-episode-title {
    font-size: 20px;
  }
  
  #tvshow-episode-air-date {
    color: #ff9941;
  }  
  
  #tvshow-episode-run-time {
    text-align: right;
    margin-top: -33px;
  }
  
  #tvshow-episode-overview {
    margin-top: 40px;
    font-weight: 400;
  }
</style>
