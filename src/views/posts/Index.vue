<template>
  <div>
    <h1>{{ header }}</h1>
    <div v-for="post in posts" :key="post.id">
      <div class="post">
        <router-link :to="{ name: 'PostById', params: { id: post.id } }">
          {{ post.title }}
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
const axios = require("axios").default;

export default {
  data() {
    return {
      posts: null,
      header: null
    };
  },

  methods: {},
  // Callback v.s. Promise v.s. Async-Await
  async mounted() {
    this.header = "All Posts in mounted";

    // axios.get('http://localhost:8000/api/posts')
    //      .then(response => {
    //       console.log(response);
    //       this.posts = response.data;
    //      });

    let response = await axios.get("http://localhost:8000/api/posts");
    this.posts = response.data;
    console.log(response.data);
  }
};
</script>

<style>
.post {
  margin: 20px 0;
}
</style>
