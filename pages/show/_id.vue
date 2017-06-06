
<template>
  <div class="container">
    <Affix/>

    <div class="content">
      <!-- Search Bar -->
     <searchBar/>
      <!-- Top banner of the tvshow -->
      <div class="testtest" v-if="!searchDone">
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
              <img @click="followShow" :src="followPath" id="tvshow-follow-btn"/>
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
          <p v-if="!seen" class="text-light">{{actorName}}</p>
          <p v-if="!seen">{{actorBio}}</p>

        </div>
        <div class="tvshow-cast">
          <div id="tvshow-cast-text">
            The cast <img src="~assets/cast.png" id="tvshow-cast-icon"/>
          </div>
          <div  id="tvshow-actor-photo-container">
            <li v-for="actor in cast" class="tvshow-actor-photo">
              <div id="tvshow-actor-photo-element">

              <img @mouseover="setBio(actor), seen=false" @mouseleave="seen = true" id="tvshow-cast-poster" :title="actor.name" :alt="actor.name" :src="'https://image.tmdb.org/t/p/original/'+actor.profile_path"/></div></li>
            <div>
              <li v-for="actor in cast" class="tvshow-actor-name">{{actor.name}}</li>
            </div>
          </div>
        </div>
      </div>

      <!-- Details of episodes and seasons -->
      <div class="tvshow-season-div">
      <div @click="showEpisodesFn, showEpisodes = true" @mouseleave="showEpisodes = false" class="seasons-gradient">
        <div  class="tvshow-seasons-episodes">
          <ul>
            <li  id="tvshow-season-list" v-for="(season, index) in movie.seasons">
              <div  class="tvshow-season-img"><p  id="tvshow-season-text">season {{season.season_number}} {{season.episode_count}} episodes</p><img  :src="img_path + season.poster_path" id="tvshow-season-poster"/></div>
              <ul>
                <div id="tvshow-episode-list" v-if="showEpisodes">
                  <li @click="setOverviewM(season, n); saw = true"  v-for="n in season.episode_count" class="tvshow-episode-number"><p :v-show="showEpisodes">{{n}}</p></li>
                </div>
              </ul>
            </li>
          </ul>
        </div>
      </div>
    </div>
      <div class="tvshow-episode-details">
        <div class="tvshow-episode-content">
          <div id="tvshow-episode-img">
            <!-- <img @click="followEpisode()" v-if="saw" :src="followEpisodePath" id="tvshow-saw-btn"/>-->
            <img id="tvshow-episode-poster" :src="episodePoster"/>
          </div>
          <div id="tvshow-episode-text">
            <p id="tvshow-episode-title">{{episodeName}}</p>
            <p v-if="saw" id="tvshow-episode-air-date">Release date {{episodeReleasedDate}}</p>
            <p v-if="saw" id="tvshow-episode-run-time">{{movie.episode_run_time[0]}} min</p>
            <p id="tvshow-episode-overview">{{episodeOverview}}</p>
          </div>
        </div>
      </div>

      <!-- Critics of tvshow -->
      <Critics/>
    </div>
    </div>
  </div>
</template>


<!-- Scripts -->
<script>
import axios from 'axios'
import Affix from '~components/Affix.vue'
import searchBar from '~components/searchBar.vue'
import Critics from '~components/Critics.vue'

export default {
  data: () => ({
    lang: 'en-US',
    img_path: 'https://image.tmdb.org/t/p/w500/',
    apiKey: '028097eda8e5dd43094c8fcbaf15a506',
    movie: {},
    errors: [],
    cast: [],
    seen: true,
    saw: false,
    overview: '',
    episodeOverview: '',
    episodePoster: '',
    episodeName: '',
    episodeReleasedDate: '',
    episodeRunTime: '',
    seasonEpisodes: [],
    season: {},
    showUl: false,
    showOverview: false,
    actorName: '',
    actorBio: '',
    seasonPoster: '',
    seasonEpisodesNumber: 0,
    showEpisodes: false,
    results: [],
    query: '',
    searchBarShow: false,
    searchDone: false,
    followPath: '/FollowButton.png',
    episodeId: '',
    followEpisodePath: '/NotSeenButton.png'
  }),
  props: [
    'searchQuery'
  ],
  methods: {
    followEpisode: function () {
      this.followEpisodePath = '/SawButton.png'
      axios({
        method: 'put',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users/59300f38f36d2805427e6df7?apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7',
        data: {
          '$push': {followedTvEpisodes: this.episodeId}
        }
      })
    },
    unFollowEpisode: function () {
      axios({
        method: 'put',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users/59300f38f36d2805427e6df7?apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7',
        data: {
          '$remove': {followedTvEpisodes: this.episodeId}
        }
      })
    },
    followShow: function () {
      this.followPath = '/FollowedButton.png'
      axios({
        method: 'put',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users/59300f38f36d2805427e6df7?apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7',
        data: {
          '$push': {followedTvShows: this.$route.params.id}
        }
      })
    },
    unFollowShow: function () {
      this.followPath = '/FollowButton.png'
      axios({
        method: 'put',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users/59300f38f36d2805427e6df7?apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7',
        data: {
          '$remove': {followedTvShows: this.$route.params.id}
        }
      })
    },
    searchMongo: function () {
      axios({
        method: 'get',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users?q={"followedTvShows": "' + this.$route.params.id + '"}&apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7'
      }).then(response => {
        if (response.data.length === 0) {
          console.log('show is not followed')
        }console.log(response.data)
      })
    },
    showEpisodesFn: function (event) {
      console.log(event.targetVM)
    },
    setOverviewM: function (season, n) {
      console.log(season)
      console.log(n)
      axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/season/' + season.season_number + '?api_key=' + this.apiKey + '&language=' + this.lang)
      .then(response => {
        // JSON responses are automatically parsed.
        console.log(response.data)
        this.episodeOverview = response.data.episodes[n - 1].overview
        this.episodePoster = 'https://image.tmdb.org/t/p/w500/' + response.data.episodes[n - 1].still_path
        this.episodeName = response.data.episodes[n - 1].name
        this.episodeRunTime = response.data.episodes[n - 1].overview
        this.episodeReleasedDate = response.data.episodes[n - 1].air_date
        this.episodeId = response.data.episodes[n - 1].id
        console.log(this.episodeId)
      })
      .catch(e => {
        this.errors.push(e)
      })
    },
    setBio: function (actor) {
      axios.get('https://api.themoviedb.org/3/person/' + actor.id + '?api_key=' + this.apiKey + '&language=' + this.lang)
      .then(response => {
        // JSON responses are automatically parsed.
        this.actorName = response.data.name
        this.actorBio = response.data.biography
      })
      .catch(e => {
        this.errors.push(e)
      })
    },
    searchEpisodes: function (index) {
      axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/season/' + index + '?api_key=' + this.apiKey + '&language=' + this.lang)
      .then(response => {
        // JSON responses are automatically parsed.
        this.seasonEpisodesNumber = response.data.episodes.length
      })
      .catch(e => {
        this.errors.push(e)
      })
    }
  },
  components: {
    Affix,
    searchBar,
    Critics
  },
  watch: {
    '$route' (to, from) {
      axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '?api_key=' + this.apiKey + '&language=' + this.lang)
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
      axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/credits?api_key=' + this.apiKey + '&language=' + this.lang)
      .then(response => {
        // JSON responses are automatically parsed.
        this.cast = response.data.cast
      })
      .catch(e => {
        this.errors.push(e)
      })
      // datas of the tvshow seasons
      // for i=1  to this.seasons
      // apikey
      axios.get('https://api.themoviedb.org/3/person/122616?api_key=' + this.apiKey + '&language=' + this.lang)
      .then(response => {
        // JSON responses are automatically parsed.
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
      url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Users?q={"followedTvShows": "' + this.$route.params.id + '"}&apiKey=f-uDQagLij0gzft6G5473mVMsawV6Yy7'
    }).then(response => {
      if (response.data.length !== 0) {
        this.followPath = '/FollowedButton.png'
        console.log('show is not followed')
      }console.log(response.data)
    })
    // datas of the global tvshow
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '?api_key=' + this.apiKey + '&language=' + this.lang)
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
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/credits?api_key=' + this.apiKey + '&language=' + this.lang)
    .then(response => {
      // JSON responses are automatically parsed.
      this.cast = response.data.cast
    })
    .catch(e => {
      this.errors.push(e)
    })
    // datas of the tvshow seasons
    // for i=1  to this.seasons
    // apikey
    axios.get('https://api.themoviedb.org/3/person/122616?api_key=' + this.apiKey + '&language=' + this.lang)
    .then(response => {
      // JSON responses are automatically parsed.
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
    padding-top: 50px;
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

  #tvshow-actor-photo-element {
      width: 130px;
      height: 170px;
      overflow: hidden;
    }

  .tvshow-actor-photo {
    display: inline-block;
    padding-left: 0px;
  }

  #tvshow-cast-poster {
    width: 130px;
    height: auto;
    cursor:zoom-in;
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
    width: 100%;
    background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.8) 0%, rgba(255, 255, 255, 0) 100%);
    position: relative;
    display: inline-block;
    vertical-align: top;
    cursor:pointer;
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
    background-color: #262835;
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
  .tvshow-critics {
      margin: 20px;
      padding: 30px 35px;
      background-color: #161C28;
    }

    #tvshow-critics-text {
       color: white;
      font-size: 12px;
      font-weight: 800;
      margin-top: -5px;
      margin-left: -15px;
      margin-bottom: 20px;
    }

    #tvshow-critics-icon {
      width: 8px;
      margin-right: 5px;
    }

    .tvshow-critics-element {

    }

    #tvshow-critics-show-name {
      font-size: 20px;
    }

    #tvshow-critics-by {
      display: inline-block;
      margin-right: 5px;
      font-weight: 400;
      font-size: 16px;
    }
    #tvshow-critics-user-name {
      display: inline-block;
      color: #ff9941;
      font-size: 16px;
    }

    #tvshow-critics-rating {
      text-align: right;
      margin-top: -35px;
      margin-bottom: 10px;
    }

    #tvshow-critics-rating-text {
      font-size: 35px;
    }

    #tvshow-critics-likes {
      display: inline-block;
      width: 100%;
      text-align: right;
      margin-top: 10px;
    }

    .tvshow-critics-likes-icon {
      width: 20px;
      height: auto;
      margin-left: 15px;
      margin-top: 10px;
      display: inline-block;
    }

    .tvshow-critics-likes-text {
      display: inline-block;
      vertical-align: super;
      margin-left: 5px;
    }
    .tvshow-season-div {
    height: 300px;
    overflow-y: scroll;
    white-space: pre-wrap;
    width: 35%;
    display: inline-block;
    vertical-align: top;
  }
</style>
