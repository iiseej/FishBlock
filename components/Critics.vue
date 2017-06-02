<template lang="html">
  <div class="tvshow-critics">
    <div id="tvshow-critics-text">
      <img src="~assets/critics.png" id="tvshow-critics-icon"/> Critics
    </div>
    <div class="tvshow-critics-arrow">
      <button @click="prevCritic"type="button" name="button" id="shows-previous-btn"></button>
    </div>
    <div class="tvshow-critics-element">
      <div>
        <p id="tvshow-critics-show-name">{{showName}}</p>
        <p id="tvshow-critics-by">By</p>
        <a href="route">
          <p id="tvshow-critics-user-name">{{criticUser}}</p>
        </a>
      </div>
      <div id="tvshow-critics-rating"><p id="tvshow-critics-rating-text">{{showNote}}/10</p></div>
      <p>{{criticText}}</p>
      <div id="tvshow-critics-likes">
        <a href="route">
          <img src="~assets/like.png" class="tvshow-critics-likes-icon"/>
        </a>
        <p class="tvshow-critics-likes-text">42</p>
        <a href="route">
          <img src="~assets/dislike.png" class="tvshow-critics-likes-icon"/>
        </a>
        <p class="tvshow-critics-likes-text">6</p>
      </div>
      <button @click="nextCritic"type="button" name="button" id="shows-next-btn"></button>
    </div>
  </div>
</template>


<!-- Scripts -->
<script>
  import axios from 'axios'
  export default {
    data () {
      return {
        apiKeyMongo: 'f-uDQagLij0gzft6G5473mVMsawV6Yy7',
        criticUser: '',
        criticText: '',
        showName: '',
        showNote: '',
        critics: {},
        index: 0
      }
    },
    methods: {
      updateCritic: function () {
      },
      prevCritic: function () {
        if (this.index === 0) {
          console.log('no previous critics')
          return
        } this.index--
        axios({
          method: 'get',
          url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Shows?apiKey=' + this.apiKeyMongo
        }).then(response => {
          this.critics = response.data[0].critics[0]
          this.criticUser = response.data[0].critics[this.index].user
          this.criticText = response.data[0].critics[this.index].review
          this.showNote = response.data[0].critics[this.index].note
          this.showName = response.data[0].name
        })
      },
      nextCritic: function () {
        console.log('next critic')
        this.index++
        axios({
          method: 'get',
          url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Shows?apiKey=' + this.apiKeyMongo
        }).then(response => {
          this.critics = response.data[0].critics[0]
          this.criticUser = response.data[0].critics[this.index].user
          this.criticText = response.data[0].critics[this.index].review
          this.showNote = response.data[0].critics[this.index].note
          this.showName = response.data[0].name
        })
      }
    },
    created () {
      axios({
        method: 'get',
        url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Shows?apiKey=' + this.apiKeyMongo
      }).then(response => {
        this.critics = response.data[0].critics[0]
        this.criticUser = response.data[0].critics[0].user
        this.criticText = response.data[0].critics[0].review
        this.showNote = response.data[0].critics[0].note
        this.showName = response.data[0].name
      })
    }
  }
</script>


<!-- CSS in order of apparition -->
<style lang="css" scoped>
  .tvshow-critics-arrow {
    width: 100%;
  }

  #shows-previous-btn {
    width: 18px;
    height: 30px;
    border: none;
    outline: none;
    background-size: cover;
    background-color: rgba(0, 0, 0, 0.0);
    background-image: url('~assets/previous.png');
    cursor: pointer;
    -ms-transform: rotate(90deg); /* IE 9 */
    -webkit-transform: rotate(90deg); /* Chrome, Safari, Opera */
    transform: rotate(90deg);
    margin-left: auto;
    margin-right: auto;
    display: block;
  }

  #shows-next-btn {
    width: 18px;
    height: 30px;
    border: none;
    outline: none;
    background-size: cover;
    background-color: rgba(0, 0, 0, 0.0);
    background-image: url('~assets/next.png');
    cursor: pointer;
    -ms-transform: rotate(90deg); /* IE 9 */
    -webkit-transform: rotate(90deg); /* Chrome, Safari, Opera */
    transform: rotate(90deg);
    margin-left: auto;
    margin-right: auto;
    display: block;
  }
</style>
