<template>
    <div>
        <p><strong>Author:</strong> {{ post.author }}</p>
        <p><strong>Content:</strong> {{ post.content }}</p>
        <p><strong>Created At:</strong> {{ post.created_at }}</p>
        <p><strong>Updated At:</strong> {{ post.updated_at }}</p>
        <p><strong>Published At:</strong> {{ post.published_at }}</p>
   </div>
  </template>

  <script>
  export default {
    name: "PostCard",
    props: {
        post: {
        type: Object,
                default: () => {
                    return {};
                },
        },
    },
  };
  </script>

  <style scoped>
  h1 {
    font-size: 2em;
    margin-bottom: 1em;
  }
  h2 {
    margin: 0.5em 0;
  }
  ul {
    list-style-type: none;
    padding: 0;
  }
  li {
    margin-bottom: 2em;
    padding: 1em;
    border: 1px solid #ccc;
    border-radius: 5px;
  }
  </style>
