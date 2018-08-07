<template>
  <div class="contents like-channels">
    <p class="property">好きなチャンネル：</p>
    <ul v-if="channels">
      <li v-for="channel in channels" class="channel">
        <p>{{channel}}</p>
      </li>
    </ul>
  </div>
</template>
<script>
  export default {
    props: ["channels"],
    data(){
      return {
      }
    }
  }
</script>
