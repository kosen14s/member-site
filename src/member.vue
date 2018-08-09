<template>
  <div class="container member">
    <ul class="member_list">
      <li v-for="member in filteredView" :key="member.id" class="member_list_item">
        <div>
          <div class="member-header">
            <img class="member-icon" :src="'./src/assets/icons/'+member.icon" :alt="'icon'">
            <div class="member-name">
              <h2>{{member.name}}</h2>
              <LinkList :links="member.links"></LinkList>
            </div>
          </div>

          <div class="contents origin-box">
            <p class="origin" v-show="member.origin">{{member.origin}}</p>
          </div>

          <div class="contents area-box">
            <p class="property-name">生息地：</p>
            <p class="property" v-show="member.area">{{member.area}}</p>
          </div>

          <div class="self-info-box">
            <p class="property-name">コメント：</p>
            <p v-for="selfinfo in member.self_introduction" :key="selfinfo.id" class="self-info">
              {{selfinfo}}
            </p>
          </div>

          <ChannelList :channels="member.channels" v-on:addchanneltag="addChannelTag"></ChannelList>
        </div>
      </li>
      <div class="more-display" v-show="filteredView.length<this.filter.search_hit && filteredView.length>0">
        <button @click="filter.display = filter.display+3">さらに表示</button>
      </div>
    </ul>
    <div v-show="filteredView.length==0">
      フィルタリングの結果、ヒットしませんでした。
    </div>
  </div>
</template>
<script>
  import LinkList from './components/link-list.vue'
  import ChannelList from './components/channel-list.vue'
  export default {
    props: ["filter","members"],
    data(){
      return {
      }
    },
    components: {
      LinkList: LinkList,
      ChannelList: ChannelList
    },
    methods: {
      addChannelTag(channeltag){
        if (this.filter.channeltags.indexOf(channeltag) == -1){//既存のtagに存在しなければ追加
          this.$parent.filter.channeltags.push(channeltag);
        }else{
          for (let i = 0; i < this.filter.channeltags.length; i++) {//既存のtagに存在してたら削除
            if(this.filter.channeltags[i] == channeltag){
              this.filter.channeltags.splice(i, 1);
            }
          }
        }
      }
    },
    computed: {
      filteredView() {
        var seachmembers = [];
        var display_vol = this.filter.display-1
        var hit = 0;

        for (var i in this.members) {
            var member = this.members[i];
            var self_intro_txt = "";
            var channeltag_link = [];

            for (var j in member.self_introduction) {
                self_intro_txt = self_intro_txt + member.self_introduction[j];
            }
            for (var j in member.channels){
              if(this.filter.channeltags.indexOf(member.channels[j]) !== -1){
                channeltag_link.push(true);
              }
            }
            console.log(self_intro_txt);
            if((member.name.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1 ||
              member.origin.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1 ||
              member.area.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1 ||
              self_intro_txt.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1)
              && (channeltag_link.length==this.filter.channeltags.length)) {
              if(display_vol >= hit){
                seachmembers.push(member);
              }
              hit++;
            }
        }
        this.$parent.filter.search_hit = hit;
        this.$parent.filter.member_viewlength = seachmembers.length;
        return seachmembers;
      }
    }
  }
</script>
<style lang="scss">
.member {
  ul.member_list {
    display: flex;
    flex-wrap: wrap;
    li.member_list_item {
      margin: 4px;
      padding: 36px;
      border-radius: 10px;
      width: 28%;
      background: #ecf0ef;
      .member-header {
        display:flex;
        flex-wrap: nowrap;
        .member-icon {
          width:100px;
          height:100px;
          border: 1px solid #ddd;
          border-radius: 20px;
          margin-right: 20px;
        }
        .member-name{
          h2 {
            margin: 0;
            display: block;
          }

        }

      }
      .contents {
        display: flex;
        flex-wrap: wrap;
        margin: 0;
      }
      .property-name {
          font-size: 1.5rem;
          line-height: 2.8rem;
          display: block;
          color: #58615f;
          margin: 0;
        }
      .property {
        display: inline-flex;
        flex-wrap: wrap;
        font-size: 1.8rem;
        line-height: 2.8rem;
        margin: 0;
        width: auto;
        padding-left: .5rem;
      }
      .origin-box {
        margin-top: 1.5rem;
        .origin {
          display: inline-flex;
          flex-wrap: wrap;
          font-size: 1.8rem;
          line-height: 2.8rem;
          margin: 0;
          width: auto;
          font-size: 2rem;
        }
      }
      .area-box {
        margin-top: .5rem;
      }

      .self-info-box {
        margin: 1.5rem 0;
        .self-info_property {
          font-size: 1.5rem;
          line-height: 2.8rem;
          display: block;
          color: #333;
          margin: 1.5rem 0 0;
        }
        .self-info {
          margin: 0 0 .5rem;
          font-size: 1.7rem;
          line-height: 2.8rem;
          padding-left:1rem;
        }
      }
    }
    .more-display {
      width: 100%;
      text-align: center;
      margin-bottom: 200px;
      button {
        margin: 20px;
        width: 200px;
        font-family: "Noto Sans Japanese";
        font-size: 1.6rem;
        line-height: 50px;
        background: #ecf0ef;
        border: none;
        border-radius: 5px;
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
  }
}
</style>
