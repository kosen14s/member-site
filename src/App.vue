<template>
  <div id="app">
    <header>
      <div class="container">
        <img src="kosen14s_logo" alt="14slogo">
        <div class="title">
          <h1>#profile</h1>
          <p>kosen14sの、{{this.members.length}}人のメンバーを紹介します。</p>
        </div>
        <input v-model="search" placeholder="キーワード検索">
        <div>
          <button @click="display=6">6人表示</button>
          <button @click="display=12">12人表示</button>
        </div>
      </div>
    </header>

    <MemberList :display="display" :members="members" :search="search" :channels="channels"></MemberList>
  </div>
</template>

<script>
import MemberList from './member.vue'
import axios from 'axios'

export default {
  name: 'app',
  data() {
    return {
      display: 6,
      search: "",
      channels: [],
      members: []
    }
  },
  components: {
    MemberList: MemberList
  },
  mounted () {
    var that = this
    axios.get('./src/json/members.json')
      .then(function (response) {
          that.members = response.data;
          console.log("read json");
      })
      .catch(function (error) {
          console.log(error);
      });
  }
}
</script>

<style lang="scss">
body {
  font-size: 62.5%;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 30px;
  font-size: 1.1rem;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.container {
  width: 1500px;
  margin:auto;
}
</style>
