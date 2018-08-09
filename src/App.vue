<template>
  <div id="app">
    <header>
      <div class="container">
        <div class="title">
          <a href="./" class="sub-title">
            <img src="../src/assets/kosen14s_logo.png" alt="logo">
            <h2>kosen14s</h2>
          </a>
          <h1>#profile</h1>
        </div>
        <p class="discription">kosen14sの、{{this.members.length}}人のメンバーを紹介します。</p>
      </div>
    </header>
    <section class="filter">
      <div class="container">
          <div class="search-box">
            <input class="filter-search" v-model="filter.search" placeholder="キーワード検索">
            <button class="filter-display" @click="filter.display=6">6人表示</button>
            <button class="filter-display" @click="filter.display=12">12人表示</button>
          </div>
          <div class="filter-view">
            <ul class="filter-tag-box" v-show="filter.channeltags.length">
              <li class="channel" v-for="channeltag in filter.channeltags" :key="channeltag.id">
                <button class="channel_button" @click="removeChannelTag(channeltag)">{{"# "+channeltag}}</button>
              </li>
              <button class="channel_button channel_button_delete" @click="removeAllTag">×</button>
            </ul>

            <div class="filter-current-status">
              <p> {{this.filter.member_viewlength}} / {{this.filter.search_hit}}人表示</p>
            </div>
          </div>
        </div>
    </section>
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
    },
    removeAllTag() {
      this.filter.channeltags=[];
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

$official-twitter: #55acee;
$official-facebook: #455a9e;

$spring: #F4A7B9;
$spring-sub: #F4D0D9;
$summer: #47b2c5;
$summer-sub: #C7EFF2;
$autumn: #db9616;
$autumn-sub: #F9D7A0;
$winter: #336774;
$winter-sub: #91ABAF;

$slack-defo: #4d394b;
$slack-active: #4c9689;

html {
  font-size: 62.5%;
  height: 100%;
  font-family: "Noto Sans Japanese";
}
body {
  width: 100%;
  height: 100%;
  margin: 0;
  position: relative;
  background-color: white;
  font-size: 1.8rem;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #222;
}
::selection {
  background: $slack-active;
  color: white;
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
  margin: 0 4px;
}
a {
  color: #4c9689;
  text-decoration: none;
}
p {
  margin: 1rem 0;
  font-size: 1.8rem;
  line-height: 2.8rem;
}
.container {
  width: 1500px;
  margin:auto;
}
header {
  background: #4c9689;
  color: white;
  padding: 42px 0 24px;
  .title {
    a.sub-title {
      display: inline-flex;
      flex-wrap: nowrap;
      transition: .1s ease-out;
      color: white;
      &:hover{
        opacity: .7;
      }
      img {
        width: 38px;
        height: 38px;
      }
      h2 {
        line-height: 35px;
        margin: 0;
        padding-top: 3px;
        padding-left: 10px;
        font-size: 2rem;
      }
    }
    h1 {
      margin: .5rem 0;
      font-size: 5rem;
    }
  }
}
.filter {
  margin-top: 8px;
  .search-box {
    .filter-search {
      font-family: "Noto Sans Japanese";
      font-size: 1.4rem;
      line-height: 2rem;
      border: 1px solid #a3c0b9;
      border-radius: 5px;
      padding: 4px 8px 6px;
      color: #222;
      transition: .3s ease-out;
      &::placeholder {
        color: #a3c0b9;
      }
      &:focus {
        outline:none;
        color: white;
        border-color:#4c9689;
        background: #4c9689;
      }
    }
    .filter-display {
      font-family: "Noto Sans Japanese";
      font-size: 1.4rem;
      line-height: 2rem;
      background: white;
      border: 1px solid #a3c0b9;
      border-radius: 5px;
      padding: 4px 8px 6px;
      color: #222;
      transition: .3s ease-out;
      cursor: pointer;
      &:focus {
        outline:none;
      }
      &:hover{
        border-color:#4c9689;
        background: #4c9689;
        color: white;
      }
    }
  }
  .filter-view {
    .filter-tag-box{
      margin: 4px 0;
      display: inline-block;
      padding-right: 24px;
    }
    .filter-current-status {
      font-size: 1.4rem;
      margin: 10px 0;
      p {
        margin: 0;
      }
    }
  }
}

</style>
