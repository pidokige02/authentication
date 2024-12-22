<template>
  <div>
    <h1>Dashboard</h1>
    <template v-if="!isLoading">
      <PostCard v-for="post in posts" :key="post.id" :post="post" />
    </template>
    <p v-else>Loading posts</p>
  </div>
</template>

<script>
import axios from "axios";
import PostCard from "../components/PostCard";

export default {
  components: { PostCard },
  data() {
    return {
      isLoading: true,
      posts: [],
    };
  },
  created() {
    axios.get("//localhost:8000/api/blog/posts").then(({ data }) => {
      this.posts = data.map((item) => item.fields);
      // console.log("Jinha POSTS",this.posts)
      this.isLoading = false;
    });
  },
};
</script>
