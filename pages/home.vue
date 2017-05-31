<template>
  <div class="container">
    <Affix/>
    <div class="home-content">


      <h1>{{msg}}</h1>
      <SearchBar/>

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

      <!-- Last episodes aired -->


    </div>
  </div>
</template>


<!-- Scripts -->
<script>
import Affix from '~components/Affix.vue'
import SearchBar from '~components/searchBar.vue'
export default {
  data () {
    return {
      msg: 'this is your home'
    }
  },
  components: {
    Affix,
    SearchBar
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
</style>
