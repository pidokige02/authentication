<template>
  <div>
    <h1>Dashboard</h1>
    <!-- Create Blog Post Button -->
    <router-link to="/create" class="create-post-button">
      Create Blog Post
    </router-link>

    <template v-if="!isLoading">
      <div v-for="post in posts" :key="post.id">
        <!-- Router link wrapping PostCard -->
        <router-link :to="`/post/${post.id}`" class="post-link">
          <PostCard :post="post" />
        </router-link>
      </div>
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
    axios.get("//localhost:8000/blog/api").then(({ data }) => {
      this.posts = data;
      this.isLoading = false;
    });
  },
};
</script>

<style>
/* Optional styles for links */
.post-link {
  text-decoration: none;
  color: inherit;
  display: block;
}

.create-post-button {
  display: inline-block;
  margin-bottom: 20px;
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  text-decoration: none;
  border-radius: 5px;
  text-align: center;
}

.create-post-button:hover {
  background-color: #0056b3;
}
</style>