<template>
  <div>
    <div v-for="post in posts" :key="post.id" class="post">
      <h2 class="post-title">{{ post.title.rendered }}</h2>
      <div class="post-content" v-html="post.content.rendered"></div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      posts: [],
    };
  },
  mounted() {
    this.fetchPosts();
  },
  methods: {
    fetchPosts() {
      axios
        .get("https://your-wordpress-site.com/wp-json/wp/v2/posts")
        .then((response) => {
          this.posts = response.data;
        })
        .catch((error) => {
          console.error(error);
        });
    },
  },
};
</script>

<style>
.post {
  margin-bottom: 20px;
}
.post-title {
  font-size: 24px;
  margin-bottom: 10px;
}
.post-content {
  font-size: 16px;
}
</style>
