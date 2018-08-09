<template>
  <div id="app">
    <header>
      <div class="container">
        <img src="kosen14s_logo" alt="14slogo">
        <div class="title">
          <h1>#profile</h1>
          <p>kosen14sの、{{this.members.length}}人のメンバーを紹介します。</p>
        </div>
        <input v-model="filter.search" placeholder="キーワード検索">
        <div>
          <button @click="filter.display=6">6人表示</button>
          <button @click="filter.display=12">12人表示</button>
        </div>
        <ul>
          <li v-for="channeltag in filter.channeltags" :key="channeltag.id">
            <button @click="removeChannelTag(channeltag)">{{"#"+channeltag}}</button>
          </li>
        </ul>
        <p>{{this.filter.member_viewlength}}/{{this.filter.search_hit}}人表示</p>
      </div>
    </header>
    <MemberList :filter="filter" :members="members"></MemberList>
  </div>
</template>

<script>
import MemberList from './member.vue'
import axios from 'axios'

export default {
  name: 'app',
  data() {
    return {
      filter: {
        display: 6,
        search: "",
        search_hit:0,
        member_viewlength:0,
        channeltags: [],
        all_channel_list: []
      },
      members: []
    }
  },
  components: {
    MemberList: MemberList
  },
  methods: {
    removeChannelTag(channeltag) {
      for (let i = 0; i < this.filter.channeltags.length; i++) {
        if(this.filter.channeltags[i] == channeltag){
          this.filter.channeltags.splice(i, 1);
        }
      }
    }
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
