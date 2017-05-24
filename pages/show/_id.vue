
<template>
  <div class="container">
    <Affix/>
  <div class="content">
   <div class="gradient">
    <div class="backdrop">
     <img   style="width:100%; position: relative;
    top: -50px; z-index: -10;" :src="'https://image.tmdb.org/t/p/original/'+movie.backdrop_path" alt="">
    <div class="tvshow-title">
    <p style="font-size: 50px; margin-left: 25px;"><strong>{{movie.original_name}}</strong></p>
      <p style="font-size: 20px; margin-left: 25px;"><strong>{{movie.first_air_date}}</strong></p>
      <p style="font-size: 14px; margin-top: -24px; margin-left: 70px;"><strong><li class="tvshow-genres" v-for="genre in movie.genres"> {{genre.name}}</li></strong></p>
      <p style="font-size: 14px; margin-left: 25px; margin-top: 45px;">{{movie.number_of_seasons}} seasons</p>
      <p style="font-size: 14px; margin-left: 25px; color: #ff9941;">Last episode aired {{movie.last_air_date}}</p>
                <div><a href="route"><img src="~assets/FollowButton.png" style="width:130px; height: auto; margin-top: -32px; position: absolute; right: 30px;"/></a></div>
    </div>
    </div>
    </div>
    <div class="tvshow-synopsis-cast">
       <div   class="tvshow-synopsis">
       <div  id="about"><img    src="~assets/about.png" style="width: 8px; margin-right: 5px;"/> About the show</div>
       <p  style="font-size: 20px;">254 Followers</p>
       <p  style="font-size: 20px; margin-bottom: 20px;">26 Critics</p>
        <p  v-if="seen" class="text-light" >{{overview}}</p>
        </div>
        <div class="tvshow-cast">
                 <div id="casting">The cast <img src="~assets/cast.png" style="width: 10px; margin-left: 5px;"/></div>
         <div  @click="seen = !seen" id="actor-photo-container">
          <li  v-for="actor in cast" class="actor-photo"><img  style="width: 130px; height: auto;" :src="'https://image.tmdb.org/t/p/original/'+actor.profile_path"/></li>
                    <div class="actor-name-container">
          <li v-for="actor in cast" class="actor-name" style="width: 130px; text-align: center;">{{actor.name}}</li></div></div>

        </div>
        </div>
    <ul>
      <li v-for="i in movie.number_of_seasons">
        season {{i}}
      </li>
    </ul>
  </div>
</div>
</template>

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
    overview: ''
  }),
  components: {
    Affix
  },

  // Fetches posts when the component is created.
  created () {
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
    axios.get('https://api.themoviedb.org/3/tv/' + this.$route.params.id + '/credits?api_key=' + this.apiKey + '&language=en-US')
    .then(response => {
      // JSON responses are automatically parsed.
      this.cast = response.data.cast
    })
    .catch(e => {
      this.errors.push(e)
    })
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
  height: 2000px;
  margin-left: 220px;
  justify-content: center;
  position: relative;
}

.backdrop {
  width: 100%;
  height: 200px;
  overflow: hidden;
  position: relative;
}

.gradient {
background-image: -webkit-linear-gradient(left, rgba(0, 0, 0, 0.8) 0%, rgba(255, 255, 255, 0) 100%);
 position: relative;
}

.tvshow-title {
  z-index: 100;
  position: absolute;
  top: 10px;
  width: 100%;
}

.tvshow-genres {
  display: inline-block;
  padding-left: 20px;
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

#about {
  color: white;
  font-size: 12px;
  font-weight: 800;
  margin-top: -5px;
  margin-left: -15px;
  margin-bottom: 20px;
}

#casting {
  color: white;
  font-size: 12px;
  font-weight: 800;
  margin-top: -5px;
  margin-right: -15px;
  margin-bottom: 20px;
  text-align: right;
}

.tvshow-cast {
  display: inline-block;
  width: 60%;
  padding-left: 20px;
  vertical-align: top;
}

.actor-name {
  display: inline-block;
  padding-left: 0px;
  color: white;
  margin-bottom: 10px;
  font-size: 11px;
}

.actor-photo {
  display: inline-block;
  padding-left: 0px;
}

#actor-photo-container {
  overflow-x: scroll;
  white-space: nowrap;
  max-width: 800px;
  margin-right: 0px;
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

.text-light {
  font-weight: 400;
}
</style>
