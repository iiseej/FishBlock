<template lang="html">
  <div class="tvshow-critics">
    <div id="tvshow-critics-text">
      <img src="~assets/critics.png" id="tvshow-critics-icon"/> Critics
    </div>
    <div id="tvshow-critics-arrows">
      <button @click="prevCritic"type="button" name="button" id="shows-previous-btn"></button>
      <button @click="nextCritic"type="button" name="button" id="shows-next-btn"></button>
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
    </div>
</div>
</template>

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
      index: 0
    }
  },
  methods: {
    prevCritic: function () {
      if (this.index === 0) {
        return
      } this.index--
    },
    nextCritic: function () {
    }
  },
  created () {
    axios({
      method: 'get',
      url: 'https://api.mlab.com/api/1/databases/fishblock/collections/Shows?apiKey=' + this.apiKeyMongo
    }).then(response => {
      this.showName = response.data[this.index].name
      this.criticUser = response.data[this.index].critics[this.index].user
      this.criticText = response.data[this.index].critics[this.index].review
      this.showNote = response.data[this.index].critics[this.index].note
    })
  }
}
</script>

<style lang="css" scoped>
#tvshow-critics-arrow {
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
  position: fixed;
  margin-top: 40vh;
  margin-left: 20px;
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
  position: fixed;
  right: 0px;
  margin-top: 40vh;
  margin-right: 20px;
}
</style>
