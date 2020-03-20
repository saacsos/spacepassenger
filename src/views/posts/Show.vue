<template>
  <div>
    <h1>Post {{ id }}</h1>
    <h2>{{ post.title }}</h2>
    <h3>By {{ post.user.name }}</h3>
    <div>
      {{ post.detail }}
    </div>

    <hr />
    <div>
      <label for="title">Edit Title</label>
      <input type="text" v-model="post.title" />
      <button @click="onSubmit">Edit</button>
    </div>
  </div>
</template>

<script>
const axios = require("axios").default;

export default {
  data() {
    return {
      id: null,
      post: {
        title: null,
        user: {
          name: null
        },
        detail: null
      }
    };
  },
  methods: {
    async onSubmit() {
      let response = await axios.post(
        "http://localhost:8000/api/posts/" + this.id,
        {
          _method: "PUT",
          title: this.post.title,
          detail: this.post.detail
        }
      );
      console.log(response);
    }
  },
  async mounted() {
    this.id = this.$route.params.id;

    let response = await axios.get(
      "http://localhost:8000/api/posts/" + this.id
    );
    this.post = response.data;
  }
};
</script>
