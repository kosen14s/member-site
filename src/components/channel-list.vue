<template>
  <div class="contents channels">
    <p class="property-name">出没チャンネル：</p>
    <ul class="property" v-if="channels">
      <li v-for="channel in channels" :key="channel.id" class="channel">
        <button @click="$emit('addchanneltag', channel)" class="channel_button">{{"# "+channel}}</button>
      </li>
    </ul>
  </div>
</template>
<script>
  export default {
    props: ["channels","channeltags"],
    data(){
      return {
      }
    }
  }
</script>
<style lang="scss">
  .channel {
    display: inline-block;
    margin: 0;
  }
  .channel_button {
    //background: #4d394b;
    background: #4c9689;
    font-family: "Noto Sans Japanese";
    margin: 1px;
    font-size: 1.4rem;
    padding: 0.4rem 1rem 0.5rem;
    border: none;
    color:white;
    border-radius: 5px;
    transition: .3s ease-out;
    cursor: pointer;
    &:hover {
      background: #64b3a4;
    }
  }
  .channel_button_delete {
    background: #864242;
    &:hover {
      background: #b36565;
    }
  }

</style>

