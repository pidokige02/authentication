<template>
  <div class="post-details">
    <!-- Post List 버튼 -->
    <router-link to="/dashboard" class="btn btn-primary">Post List</router-link>
    <!-- 게시물 제목 -->
    <h2>{{ post.title }}</h2>
    <!-- 게시물 메타 정보 -->
    <p>created: {{ formatDate(post.created_at) }}</p>
    <p>updated: {{ formatDate(post.updated_at) }}</p>
    <p>published: {{ formatDate(post.published_at) }}</p>
    <p>author: {{ post.author }}</p>
    <!-- 게시물 내용 -->
    <p>{{ post.content }}</p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      post: {}, // 게시물 데이터를 저장
    };
  },
  created() {
    // URL에서 게시물 ID 가져오기
    const postId = this.$route.params.id;
    console.log("Jinha postId", postId)
    // API 호출하여 게시물 데이터 가져오기
    axios
      .get(`http://localhost:8000/blog/api/${postId}/`)
      .then(({ data }) => {
        this.post = data;
      })
      .catch((error) => {
        console.error("Error fetching post details:", error);
      });
  },
  methods: {
    // 날짜 형식 변환 메서드
    formatDate(date) {
      if (!date) return "N/A";
      return new Date(date).toLocaleString("en-US", {
        year: "numeric",
        month: "long",
        day: "numeric",
        hour: "numeric",
        minute: "numeric",
        second: "numeric",
      });
    },
  },
};
</script>
<style>
.post-details {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}
.btn {
  display: inline-block;
  padding: 10px 20px;
  margin-bottom: 20px;
  background-color: #007bff;
  color: #fff;
  text-decoration: none;
  border-radius: 4px;
  text-align: center;
}
.btn:hover {
  background-color: #0056b3;
}
h2 {
  font-size: 24px;
  margin-bottom: 10px;
}
p {
  font-size: 16px;
  margin: 5px 0;
}
</style>
