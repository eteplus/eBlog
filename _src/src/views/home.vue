<template>
<div class="posts">
  <div class="page-subhead">最新文章(lastest articles)</div>
  <transition-group tag="div" name="list" class="pure-g">
    <post v-for="(post, index) in posts" :author="post.author" :title="post.title" :description="post.description" :date="post.date" :tags="post.tags" :url="post.url" :key="index"/>
  </transition-group>
</div>
</template>

<script>
import { mapState } from 'vuex';
import Post from '../components/Post';

export default {
  computed: mapState(['posts']),
  beforeRouteEnter(to, from, next) {
    next((vm) => {
      if (!vm.posts.length) {
        vm.$store.dispatch('FETCH', 'posts');
      }
    });
  },
  components: {
    Post
  }
};
</script>

<style>
.post-images {
  margin: 1em 0;
}

.post-image-meta {
  margin-top: -3.5em;
  margin-left: 1em;
  color: #fff;
  text-shadow: 0 1px 1px #333;
}
</style>
