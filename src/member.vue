<template>
  <div class="container member">
    <p>{{filteredView.length}}/{{this.search_hit}}人表示</p>
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
          <ChannelList :channels="member.like_channels"></ChannelList>
          
          <p v-for="selfinfo in member.self_introduction" :key="selfinfo.id" class="self-info">
            {{selfinfo}}
          </p>

        </div>
      </li>
      <li v-show="filteredView.length<this.search_hit && filteredView.length>0">
        <button @click="display = display+3">さらに表示</button>
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
    props: ["display","members","search","channels"],
    data(){
      return {
        search_hit:0
      }
    },
    components: {
      LinkList: LinkList,
      ChannelList: ChannelList
    },
    computed: {
      filteredView() {
        var seachmembers = [];
        var display_vol = this.display-1
        this.search_hit = 0;

        for (var i in this.members) {
            var member = this.members[i];
            var self_intro_txt = "";
            for (var j in member.self_introduction) {
                self_intro_txt = self_intro_txt + member.self_introduction[j];
            }
            console.log(self_intro_txt);
            
            if(member.name.toLowerCase().indexOf(this.search.toLowerCase()) !== -1 ||
              member.origin.toLowerCase().indexOf(this.search.toLowerCase()) !== -1 ||
              member.area.toLowerCase().indexOf(this.search.toLowerCase()) !== -1 ||
              self_intro_txt.toLowerCase().indexOf(this.search.toLowerCase()) !== -1) {
              if(display_vol >= this.search_hit){
                seachmembers.push(member);
              }
              this.search_hit++;
            }
        }
        return seachmembers;
      },
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
