<template>
  <div class="contents like-channels">
    <p class="property">出没チャンネル：</p>
    <ul v-if="channels">
      <li v-for="channel in channels" :key="channel.id" class="channel">
        <button @click="$emit('addchanneltag', channel)">{{"#"+channel}}</button>
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
