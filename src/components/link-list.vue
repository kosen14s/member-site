<template>
  <div class="link-list">
    <ul>
      <li v-if="links.site_url">
        <a :href="links.site_url">
          <img src="site_icon" alt="site">
        </a>
      </li>
      <li v-if="links.twitter_id">
        <a :href="'https://twitter.com/'+ links.twitter_id">
          <img src="twitter_logo" alt="twitter">
        </a>
      </li>
      <li v-if="links.facebook_id">
        <a :href="'https://www.facebook.com/'+ links.facebook_id">
          <img src="facebook_logo" alt="facebook">
        </a>
      </li>
      <li v-if="links.instagram_id">
        <a :href="'https://www.instagram.com/'+links.instagram_id">
          <img src="instagram_logo" alt="instagram">
        </a>
      </li>
      <li v-if="links.github_id">
        <a :href="'https://github.com/'+ links.github_id">
          <img src="github_logo" alt="github">
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: ["links"],
    data(){
      return {
      }
    }
  }
</script>