<template>
  <div class="container">
    <Affix/>
    <div class="home-content">
<<<<<<< HEAD


      <h1>{{msg}}</h1>

      <!-- Carousel of tvshows -->
=======
     <div  :searchQuery="query" class="search">
        <input type="text" name="" value="" v-model="query" placeholder="search shows or people">
        <img @click="search" style="height:30px;width:auto;" src="~assets/searchIcon.png" alt="">
      </div>
      
      <!-- Carousel of tvshows --> 
>>>>>>> 44c4b28c75c2cbdcf0ade883c852b0e5bcb8a289
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
<<<<<<< HEAD

      <!-- Last episodes aired -->

=======
      
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
              </div>
            </div>
          </div> 
        </div>
>>>>>>> 44c4b28c75c2cbdcf0ade883c852b0e5bcb8a289

    </div>
  </div>
</template>


<!-- Scripts -->
<script>
<<<<<<< HEAD
import Affix from '~components/Affix.vue'
export default {
  data () {
    return {
      msg: 'this is your home'
=======
  import Affix from '~components/Affix.vue'
  import axios from 'axios'

  export default {
    data: () => ({
      img_path: 'https://image.tmdb.org/t/p/w500/',
      movies: [],
      errors: []
    }),
    components: {
      Affix
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
>>>>>>> 44c4b28c75c2cbdcf0ade883c852b0e5bcb8a289
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
    height: 100vh;
    margin-left: 220px;
    z-index: 0;
    position: relative;
  }

  #home-carousel {
    display: flex;
    margin-top: 50px;
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
    width: 60%;
    margin-left: -50px;
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
</style>
