<template lang="html">
    <div id="nav-bar">
     <div id="nav-bar-ajust">
      <div id="nav-bar-middle">
        <img src="~assets/profilPicture.jpg" alt="Profil Picture" class="rounded-picture" />
        <ul>
          <li  v-for="(item, index) in menu" @mouseover.stop="changePath(index)" @mouseleave.stop="changePathBack(index)":class="'nav-bar-selected'" >
            <div class="nav-bar-element">
              <img  style="height:20px;width:auto;" :src="item.path + item.name + 'Icon.png'" alt="">
              <nuxt-link :to="'/'+item.path_"><p>
                <p class="nav-bar-text">{{item.name}}</p></nuxt-link>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div id="nav-bar-bottom">
        <img src="~assets/klausLogo.png" alt="Klaus Logo" class="logo"/>
        <p id="night-mode"><img src="~assets/nightModeOn.png" alt="Night Mode Button" id="night-mode-on"/>{{ $t('links.nightmod') }}</p>
        <!-- <a href="route"> -->
          <div id="btn-logout">
            <traduction/>
          </div>
        </a>
      </div>
    </div>
  </template>

<script>
import traduction from '~components/traduction.vue'

export default {
  data () {
    return {
      menu: [{
        name: this.$t('links.home'),
        path: '/orangeIcons/',
        path_: 'Home'
      },
      {
        name: this.$t('links.profil'),
        path: '/orangeIcons/',
        path_: 'profil'
      },
      {
        name: this.$t('links.shows'),
        path: '/orangeIcons/',
        path_: 'shows'
      }
      // {
      //   name: this.$t('links.messages'),
      //   path: '/orangeIcons/',
      //   path_: 'messages'
      // },
      // {
      //   name: this.$t('links.settings'),
      //   path: '/orangeIcons/',
      //   path_: 'settings'
      // }
    ],
    nightmod : 'Night Mode',
    logout : 'Logout'
    }
  },
  methods: {
    changePath: function (index) {
      this.menu[index].path = '/blackIcons/'
    },
    changePathBack: function (index) {
      this.menu[index].path = '/orangeIcons/'
    }
  },
  components: {
    traduction
  },
  head () {
    return {
      nightmod: this.$t('links.nightmod'),
      logout: this.$t('links.logout')
    }
  }
}
</script>

<style lang="css">
body {
  padding: 50px;
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
}



a {
  color: #00B7FF;
}

body {
  padding: 0px;
  margin: 0px;
}

a {
  text-decoration: none;
}

p {
  font-family: 'Karla', sans-serif;
  font-size: 14px;
  font-weight: 800;
  color: white;
}

.p-light {
  font-weight: 400;
  display: inline-flex;
  padding-top: 14px;
}

ul {
  list-style: none;
  margin-left: 0;
  padding-left: 0px;
}

li {
  padding-top: 6px;
  padding-bottom: 10px;
  padding-left: 45px;
}

h1{
  color:red;
}



#nav-bar {
  width: 220px;
  height: 100%;
  background-color: #161C28;
  position: fixed;
  display: flex;
  flex-direction: column;
}

.icons {
  vertical-align: text-bottom;
  background-image: url(~assets/icons.png);
  width: 20px;
  height: 20px;
  background-repeat: no-repeat;
  background-size: 40px;
}

.nav-bar-element {
  display: inline-flex;
  align-items: center;
  vertical-align: -webkit-baseline-middle;
}

#home-icon {
  background-position: 0 0;
}

#profil-icon {
  background-position: 0 -20px;
}

#shows-icon {
  background-position: 0 -40px;
}

#messages-icon {
  background-position: 0 -60px;
}

#settings-icon {
  background-position: 0 -80px;
}

.nav-bar-selected:hover {
  background-color: #ff9941;
}

.nav-bar-text {
  padding-left: 20px;
}

.nav-bar-selected:hover .nav-bar-text {
  color: black;
}

.nav-bar-selected:hover #home-icon {
  background-position: -20px 0;
}

.nav-bar-selected:hover #profil-icon {
  background-position: -20px -20px;
}

.nav-bar-selected:hover #shows-icon {
  background-position: -20px -40px;
}

.nav-bar-selected:hover #messages-icon {
  background-position: -20px -60px;
}

.nav-bar-selected:hover #settings-icon {
  background-position: -20px -80px;
}

#nav-bar-ajust {
  margin-bottom: 50px;
}

#nav-bar-middle {
  margin-bottom: 20%;
  margin-top: 80%;
}

#nav-bar-bottom {
  position: absolute;
  bottom: 0px;
  background-color: #161C28;
}

.rounded-picture {
  overflow: hidden;
  -webkit-border-radius: 50px;
  -moz-border-radius: 50px;
  border-radius: 50px;
  width: 90px;
  height: 90px;
  display: block;
  margin: auto;
  margin-bottom: 30px;
}

.logo {
  width: 90px;
  height: auto;
  margin: auto;
  display: block;
  margin-bottom: 20px;
}

#night-mode {
  font-size: 12px;
  font-weight: 400;
  text-align: center;
  margin-bottom: 20px;
}

#night-mode-on {
  width: 30px;
  height: auto;
  vertical-align: text-bottom;
  margin-right: 15px;
}

#btn-logout {
  text-align: center;
  width: 220px;
  height: 45px;
  background-color: black;
}

#btn-logout:hover {
  background-color: #f3f3f3;
}

#btn-logout:hover .p-light{
  color: black;
  font-weight: 800;
}


#content {
  flex: 1 1 auto;
  background-color: #262835;
  height: 2000px;
  margin-left: 220px
}

</style>
