<template>
  <div class="container">

    <Affix/>

<div class="home-content">
  <searchBar/>
  <div id="space-top"></div>
    <!-- Carousel of tvshows -->
    <div class="home-carousel-gradient">
      <div id="home-carousel">

        <div class="home-carousel-side">
          <a href="show/53606" id="love">
            <div class="home-carousel-a-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-a-text">love</p>
                <p class="home-carousel-a-genre">Comedy</p>
            </div>
          </a>
        </div>
        <div class="home-carousel-side home-carousel-gradient">
          <a href="show/62560" id="mrRobot">
            <div class="home-carousel-b-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-b-text">Mr Robot</p>
                <p class="home-carousel-b-genre">Crime</p>
            </div>
          </a>
        </div>
        <div class="home-carousel-middle home-carousel-gradient">
          <a href="show/19885" id="sherlock">
            <div class="home-carousel-c-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-c-text">Sherlock</p>
                <p class="home-carousel-c-genre">Crime</p>
            </div>
          </a>
        </div>
        <div class="home-carousel-side home-carousel-gradient">
          <a href="show/63247" id="westworld">
            <div class="home-carousel-d-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-d-text">Westworld</p>
                <p class="home-carousel-d-genre">Western</p>
            </div>
          </a>
        </div>
        <div class="home-carousel-side home-carousel-gradient">
          <a href="show/60622" id="fargo">
            <div class="home-carousel-e-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-e-text">Fargo</p>
                <p class="home-carousel-e-genre">Drama</p>
            </div>
          </a>
        </div>

      </div>
    </div>

    <!-- Last episodes aired and last critics -->
      <div class="home-last-tvshows-aired-critics">
        <div class="home-last-tvshows-title">
          <div id="home-last-tvshows-text">
            <img src="~assets/lastEpisodes.png" id="home-last-tvshows-icon"/> Last episodes
          </div>
        </div>
        <div id="home-last-tvshows-content">
          <div class="home-last-tvshows-gradient">
            <li v-for="movie in movies" class="home-last-tvshows-list">
              <div class="home-last-tvshows-element">
                <img :src="img_path + movie.backdrop_path" class="home-last-tvshows-img"/>
                <div class="home-last-tvshows-background"></div>
                <nuxt-link :to="'/show/' + movie.id"><p class="home-last-tvshows-name">{{movie.name}}</p></nuxt-link>
              </div>
            </li>
          </div>
        </div>

        <div class="home-last-tvshows-critics">
          <div class="home-last-tvshows-critics-title">
            <div id="home-last-tvshows-critics-text">
              Last critics <img src="~assets/critics.png" id="home-last-tvshows-critics-icon"/>
            </div>
          </div>
          <div id="home-last-tvshows-critics-content">
            <div class="home-last-tvshows-critics-gradient">
              <div class="home-last-tvshows-critics-element"></div>
                <div class="pouet">
                  <p class="home-last-tvshows-critics-showname">{{showName1}}</p>
                  <p class="home-last-tvshows-critics-user">By {{criticUser1}}</p>
                  <p class="home-last-tvshows-critics-rating">{{showNote1}}/10</p>
                  <div class="home-last-tvshows-critics-pouet">
                    <p class="home-last-tvshows-critics-critic">{{criticText1}}</p>
                  </div>
                </div>
              <div class="home-last-tvshows-critics-element-2"></div>
              <div class="pouet2">
                  <p class="home-last-tvshows-critics-showname">{{showName2}}</p>
                  <p class="home-last-tvshows-critics-user">By {{criticUser2}}</p>
                  <p class="home-last-tvshows-critics-rating">{{showNote2}}/10</p>
                  <div class="home-last-tvshows-critics-pouet">
                    <p class="home-last-tvshows-critics-critic">{{criticText2}}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- New shows -->
      <div class="home-new-tvshows">
        <div class="home-new-tvshows-title">
          <div id="home-new-tvshows-text">
            <img src="~assets/about.png" id="home-new-tvshows-icon"/> New shows releases
          </div>
        </div>
        <div id="home-new-tvshows-content">
        </div>
      </div>
      <div class="home-new-tvshows-elements">
        <div class="home-new-tvshows-element-side">
          <a href="show/66310" id="love">
            <div class="home-carousel-f-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-a-text">StartUp</p>
                <p class="home-carousel-a-genre">Crime</p>
            </div>
          </a>
        </div>

        <div class="home-new-tvshows-element-middle">
          <a href="show/70134" id="love">
            <div class="home-carousel-g-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-a-text">Guerrilla</p>
                <p class="home-carousel-a-genre">Drama</p>
            </div>
          </a>
        </div>

        <div class="home-new-tvshows-element-side">
          <a href="show/54344" id="love">
            <div class="home-carousel-h-img"></div>
            <div class="home-carousel-texts">
                <p class="home-carousel-a-text">The Leftovers</p>
                <p class="home-carousel-a-genre">Sci-Fi</p>
            </div>
          </a>
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
  data: () => ({
    img_path: 'https://image.tmdb.org/t/p/w500/',
    apiKeyMongo: 'f-uDQagLij0gzft6G5473mVMsawV6Yy7',
    criticUser1: '',
    criticText1: '',
    showName1: '',
    showNote1: '',
    critics1: {},
    criticUser2: '',
    criticText2: '',
    showName2: '',
    showNote2: '',
    critics2: {}
  }),
  components: {
    Affix,
    searchBar
  },
  // Fetches posts when the component is created.
  created () {
    axios.get('https://api.themoviedb.org/3/tv/airing_today?api_key=028097eda8e5dd43094c8fcbaf15a506&language=en-US&page=1')
    .then(response => {
      // JSON responses are automatically parsed.
      // this.movie = response.data
      console.log(response.data.results[0])
      this.movies = response.data.results
      this.movies = this.movies.splice(0, 4)
    })
    .catch(e => {
      this.errors.push(e)
    })
    axios({
      method: 'get',
      url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Shows?apiKey=' + this.apiKeyMongo
    }).then(response => {
      this.critics1 = response.data[0].critics[0]
      this.criticUser1 = response.data[0].critics[0].user
      this.criticText1 = response.data[0].critics[0].review
      this.showNote1 = response.data[0].critics[0].note
      this.showName1 = response.data[0].name
    })
    axios({
      method: 'get',
      url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Shows?apiKey=' + this.apiKeyMongo
    }).then(response => {
      this.critics2 = response.data[0].critics[0]
      this.criticUser2 = response.data[0].critics[1].user
      this.criticText2 = response.data[0].critics[1].review
      this.showNote2 = response.data[0].critics[1].note
      this.showName2 = response.data[0].name
    })
  }
}
</script>



<!-- CSS in order of apparition -->
<style lang="css">
#container {
  display: flex;
  min-height: 100vh;
}

.home-content {
  flex: 1 1 auto;
  background-color: #262835;
  height: auto;
  margin-left: 220px;
  z-index: 0;
  position: relative;
}

#space-top {
  height: 50px;
}

#home-carousel {
  display: flex;
  margin-top: 0px;
  position: relative;
}

.home-carousel-gradient {
  background-image: -webkit-linear-gradient(bottom, rgba(0, 0, 0, 0.6) 0%, rgba(255, 255, 255, 0) 100%);
  position: relative;
}

.home-carousel-side {
  width: 18%;
  overflow: hidden;
  height: 250px;
}

.home-carousel-texts {
  width: 100%;
  height: 100%;
  margin-top: -250px;
}

.home-carousel-a-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/HomeLove.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

/* ---------- Carousel dynamiq ---------- */
.home-carousel-a-text {
  font-size: 20px;
  text-align: center;
  padding-top: 190px;
}

.home-carousel-a-genre {
  text-align: center;
}

#love:hover .home-carousel-a-genre {
  z-index: 0;
}

#love:hover .home-carousel-a-text {
  z-index: 0;
}

/* side A */
.home-carousel-a-text {
  position: relative;
  z-index: -10;
}

.home-carousel-a-genre {
  position: relative;
  z-index: -10;
}
/* side A */

.home-carousel-b-text {
  font-size: 20px;
  text-align: center;
  padding-top: 190px;
}

.home-carousel-b-genre {
  text-align: center;
}

#mrRobot:hover .home-carousel-b-genre {
  z-index: 0;
}

#mrRobot:hover .home-carousel-b-text {
  z-index: 0;
}

/* side B */
.home-carousel-b-text {
  position: relative;
  z-index: -10;
}

.home-carousel-b-genre {
  position: relative;
  z-index: -10;
}
/* side B */

.home-carousel-c-text {
  font-size: 20px;
  text-align: center;
  padding-top: 190px;
}

.home-carousel-c-genre {
  text-align: center;
}

#sherlock:hover .home-carousel-c-genre {
  z-index: 0;
}

#sherlock:hover .home-carousel-c-text {
  z-index: 0;
}

/* middle C */
.home-carousel-c-text {
  position: relative;
  z-index: -10;
}

.home-carousel-c-genre {
  position: relative;
  z-index: -10;
}
/* middle C */

.home-carousel-d-text {
  font-size: 20px;
  text-align: center;
  padding-top: 190px;
}

.home-carousel-d-genre {
  text-align: center;
}

#westworld:hover .home-carousel-d-genre {
  z-index: 0;
}

#westworld:hover .home-carousel-d-text {
  z-index: 0;
}

/* middle D */
.home-carousel-d-text {
  position: relative;
  z-index: -10;
}

.home-carousel-d-genre {
  position: relative;
  z-index: -10;
}
/* middle D */

.home-carousel-e-text {
  font-size: 20px;
  text-align: center;
  padding-top: 190px;
}

.home-carousel-e-genre {
  text-align: center;
}

#fargo:hover .home-carousel-e-genre {
  z-index: 0;
}

#fargo:hover .home-carousel-e-text {
  z-index: 0;
}

/* middle E */
.home-carousel-e-text {
  position: relative;
  z-index: -10;
}

.home-carousel-e-genre {
  position: relative;
  z-index: -10;
}
/* middle E */
/* ---------- Carousel dynamiq ---------- */

.home-carousel-b-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/HomeMrRobot.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-carousel-c-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/HomeSherlock.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-carousel-d-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/HomeWestworld.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-carousel-e-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/HomeFargo.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-carousel-middle {
  width: 28%;
}

.home-last-tvshows-gradient {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.8) 0%, rgba(0, 0, 0, 0.2) 100%);
  position: relative;
  width: 40%;
  margin-left: -50px;
}

.home-last-tvshows-aired-critics {
  margin: 20px 20px 0px 20px;
  padding: 30px 35px 0px 30px;
  background-color: #161C28;
  z-index: -20;
  position: relative;
}

.home-last-tvshows-title {
  width: 40%;
  padding-right: 10%;
}

#home-last-tvshows-text {
  color: white;
  font-size: 12px;
  font-weight: 800;
  margin-top: -5px;
  margin-left: -15px;
  margin-bottom: 20px;
}

#home-last-tvshows-icon {
  width: 10px;
  margin-right: 5px;
}

#home-last-tvshows-content {

}

.home-last-tvshows-list {
  margin: 0;
  padding: 0;
  height: 60px;
  list-style: none;
}

.home-last-tvshows-element {
  width: 100%;
  height: 60px;
  overflow: hidden;
}

.home-last-tvshows-img {
  margin-top: -10%;
  position: relative;
  z-index: -10;
}

.home-last-tvshows-background {
  width: 100%;
  height: 100%;
  background-image: url('~assets/showImg.png');
  background-size: cover;
}

.home-last-tvshows-name {
  margin-top: -290px;
  font-size: 20px;
  padding-left: 20px;
}

.home-last-tvshows-critics {

}

.home-last-tvshows-critics-title {
  margin-top: -275px;
}

#home-last-tvshows-critics-text {
  color: white;
  font-size: 12px;
  font-weight: 800;
  margin-top: -5px;
  margin-right: -15px;
  margin-bottom: 20px;
  text-align: right;
}

#home-last-tvshows-critics-icon {
  width: 10px;
  margin-left: 5px;
}

#home-last-tvshows-critics-content {
  height: 240px;
}

.home-last-tvshows-critics-gradient {
  background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.8) 0%, rgba(0, 0, 0, 0.2) 100%);
  position: relative;
  width: 68%;
  height: 240px;
  margin-right: -55px;
  float: right;
  margin-top: 2px;
}

.home-last-tvshows-critics-element {
  height: 120px;
  background-image: url(~assets/breakingbad1.jpg);
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-last-tvshows-critics-element-2 {
  height: 120px;
  background-image: url(~assets/breakingbad2.jpg);
  background-repeat: no-repeat;
  background-position: center center;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-last-tvshows-critics-showname {
  position: relative;
  z-index: 100;
}

.pouet {
  margin-top: -118px;
  margin-bottom: 20px;
  padding-left: 20px;
  padding-top: 10px;
}

.pouet2 {
  margin-top: -118px;
  margin-bottom: 52px;
  padding-left: 20px;
  padding-top: 10px;
}

.home-last-tvshows-critics-pouet {
  margin-top: 10px;
  height: 50px;
  overflow-y: scroll;
  white-space: pre-wrap;
}

.home-last-tvshows-critics-showname {
  font-size: 18px;
}

.home-last-tvshows-critics-user {
  color: #ED9A36;
}

.home-last-tvshows-critics-rating {
  float: right;
  margin-top: -40px;
  font-size: 30px;
  margin-right: 20px;
}

.home-last-tvshows-critics-critic {
  font-weight: 400;
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

.home-new-tvshows {
  margin: 20px 20px 0px 20px;
  padding: 30px 35px 0px 30px;
  background-color: #161C28;
  z-index: -20;
  position: relative;
}

.home-new-tvshows-title {
  width: 40%;
  padding-right: 10%;
}

#home-new-tvshows-text {
  color: white;
  font-size: 12px;
  font-weight: 800;
  margin-top: -5px;
  margin-left: -15px;
  margin-bottom: 20px;
}

#home-new-tvshows-icon {
  width: 8px;
  margin-right: 5px;
}

#home-new-tvshows-content {
  margin-bottom: 20px;
  padding-bottom: 15px;
}

.home-new-tvshows-elements {
  margin-top: -35px;
  margin-bottom: 30px;
  width: 100%;
  display: inline-flex;
}

.home-new-tvshows-element-side {
  width: 36%;
  overflow: hidden;
  height: 250px;
}

.home-new-tvshows-element-middle {
  width: 28%;
  overflow: hidden;
  height: 250px;
}

.home-carousel-f-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/startUp.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-carousel-a-text:hover {
  -moz-transform: scale(1.5);
  -webkit-transform: scale(1.5);
  transform: scale(1.5);
  top: -50px;
}

.home-carousel-b-text:hover {
  -moz-transform: scale(1.5);
  -webkit-transform: scale(1.5);
  transform: scale(1.5);
  top: -50px;
}

.home-carousel-c-text:hover {
  -moz-transform: scale(1.5);
  -webkit-transform: scale(1.5);
  transform: scale(1.5);
  top: -50px;
}

.home-carousel-d-text:hover {
  -moz-transform: scale(1.5);
  -webkit-transform: scale(1.5);
  transform: scale(1.5);
  top: -50px;
}

.home-carousel-e-text:hover {
  -moz-transform: scale(1.5);
  -webkit-transform: scale(1.5);
  transform: scale(1.5);
  top: -50px;
}

.home-carousel-g-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/guerilla.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}

.home-carousel-h-img {
  height: 100%;
  width: auto;
  background-image: url('~assets/leftovers.jpg');
  background-position: center center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  z-index: -10;
}
</style>
