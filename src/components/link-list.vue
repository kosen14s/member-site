<template>
  <div class="link-list">
    <ul>
      <li class="link-box" v-show="links.site_url">
        <a :href="links.site_url">
          <img class="link-icon" src="../assets/logos/site_mono.png" alt="site">
          <img class="link-icon link-icon-hover" src="../assets/logos/site.png" alt="site">
        </a>
      </li>
      <li class="link-box" v-show="links.twitter_id">
        <a :href="'https://twitter.com/'+ links.twitter_id">
          <img class="link-icon" src="../assets/logos/twitter_mono.png" alt="twitter">
          <img class="link-icon link-icon-hover" src="../assets/logos/twitter.png" alt="twitter">
        </a>
      </li>
      <li class="link-box" v-show="links.facebook_id">
        <a :href="'https://www.facebook.com/'+ links.facebook_id">
          <img class="link-icon" src="../assets/logos/facebook_mono.png" alt="facebook">
          <img class="link-icon link-icon-hover" src="../assets/logos/facebook.png" alt="facebook">
        </a>
      </li>
      <li class="link-box" v-show="links.instagram_id">
        <a :href="'https://www.instagram.com/'+links.instagram_id">
          <img class="link-icon" src="../assets/logos/instagram_mono.png" alt="instagram">
          <img class="link-icon link-icon-hover" src="../assets/logos/instagram.png" alt="instagram">
        </a>
      </li>
      <li class="link-box" v-show="links.github_id">
        <a :href="'https://github.com/'+ links.github_id">
          <img class="link-icon" src="../assets/logos/github_mono.png" alt="github">
          <img class="link-icon link-icon-hover" src="../assets/logos/github.png" alt="github">
        </a>
      </li>
      <li class="link-box" v-show="links.tumblr_id">
        <a :href="'https://'+links.tumblr_id+'.tumblr.com'">
          <img class="link-icon" src="../assets/logos/tumblr_mono.png" alt="tumblr">
          <img class="link-icon link-icon-hover" src="../assets/logos/tumblr.png" alt="tumblr">
        </a>
      </li>
      <li class="link-box" v-show="links.blog_url">
        <a :href="links.blog_url">
          <img class="link-icon" src="../assets/logos/blog_mono.png" alt="blog">
          <img class="link-icon link-icon-hover" src="../assets/logos/blog.png" alt="blog">
        </a>
      </li>
      <li class="link-box" v-show="links.youtube_url">
        <a :href="links.youtube_url">
          <img class="link-icon" src="../assets/logos/youtube_mono.png" alt="youtube">
          <img class="link-icon link-icon-hover" src="../assets/logos/youtube.png" alt="youtube">
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
<style lang="scss">
.link-list{
  display: inline-block;
  .link-box {
    margin: 0;
    padding: 0;
    padding-top: 4px;
    padding-left: -5px;
    a {
      display: block;
      position: relative;
      width: auto;
      height: auto;
      .link-icon {
        width: 50px;
        height: 50px; //54px以上でロゴ使用権利範囲内
      }
      .link-icon-hover {
        position: absolute;
        top: 0;
        left: 0;
        opacity: 0;
        transition: .3s ease-out;
        &:hover{
          opacity: 1;
        }
      }
    }
  }
}
</style>
