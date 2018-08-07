<template>
  <div class="member_list">
    <ul>
      <li v-for="member in filteredView">
        <div class="member-icon">
          <img :src="'./assets/icons/'+member.icon" :alt="'icon'">
        </div>
        <div>
          <h2>{{member.name}}</h2>
          <LinkList :links="member.links"></LinkList>

          <div class="contents">
            <p class="property">出身：</p>
            <p v-if="member.origin">{{member.origin}}</p>
          </div>
          <div class="contents">
            <p class="property">生息地：</p>
            <p v-if="member.area">{{member.area}}</p>
          </div>
          <ChannelList :channels="member.like_channels"></ChannelList>
          
          <p v-for="selfinfo in member.self_introduction" class="self-info">
            {{selfinfo}}
          </p>

        </div>
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
    props: ["members","search"],
    data(){
      return {
      }
    },
    components: {
      LinkList: LinkList,
      ChannelList: ChannelList
    },
    computed: {
      filteredView() {
        var seachmembers = [];
        for(var i in this.members) {
            var member = this.members[i];
            if(member.name.toLowerCase().indexOf(this.search.toLowerCase()) !== -1 ||
              member.origin.toLowerCase().indexOf(this.search.toLowerCase()) !== -1 ||
              member.area.toLowerCase().indexOf(this.search.toLowerCase()) !== -1 ) {
                seachmembers.push(member);
            }
        }
        return seachmembers;
      }
    }
  }
</script>
<style lang="scss">
 .contents {
   display: flex;
   .property {
     display: inline-block;
     width: auto;
   }
 }
</style>
