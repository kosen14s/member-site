<template>
  <div class="container member">
    <ul class="member_list">
      <li v-for="member in filteredView" :key="member.id" class="member_list_item">
        <div class="member-icon">
          <img :src="'./src/assets/icons/'+member.icon" :alt="'icon'">
        </div>
        <div>
          <h2>{{member.name}}</h2>
          <LinkList :links="member.links"></LinkList>

          <div class="contents">
            <p class="property">出身：</p>
            <p v-show="member.origin">{{member.origin}}</p>
          </div>
          <div class="contents">
            <p class="property">生息地：</p>
            <p v-show="member.area">{{member.area}}</p>
          </div>
          <ChannelList :channels="member.channels" v-on:addchanneltag="addChannelTag"></ChannelList>
          
          <p v-for="selfinfo in member.self_introduction" :key="selfinfo.id" class="self-info">
            {{selfinfo}}
          </p>

        </div>
      </li>
      <li v-show="filteredView.length<this.filter.search_hit && filteredView.length>0">
        <button @click="filter.display = filter.display+3">さらに表示</button>
      </li>
    </ul>
    <div v-show="filteredView.length==0">
      no result
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
        //既存のtagに存在しなければ追加
        if (this.filter.channeltags.indexOf(channeltag) == -1){
          this.$parent.filter.channeltags.push(channeltag);
        }else{
          
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
      margin: 5px;
      padding: 20px;
      width: 30%;
      background: #eee;
      .member-icon {
        img {
          width:100px;
          height:100px;
          border: 1px solid #ddd;
          border-radius: 20px;
        }
      }
    }
  }
}
</style>
