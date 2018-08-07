<template>
  <div id="app">
    <header>
      <img src="kosen14s_logo" alt="14slogo">
      <div class="title">
        <h1>#profile</h1>
        <p>kosen14sのメンバーを紹介します。</p>
      </div>
      <input v-model="search" placeholder="キーワード検索">
    </header>

    <MemberList :members="members" :search="search"></MemberList>
  </div>
</template>

<script>
import MemberList from './member.vue'
import axios from 'axios'

export default {
  name: 'app',
  data() {
    return {
      search: "",
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

</style>
