<template>
  <div class="posts-new">
    <h1>New Post</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>
    
    <form v-on:submit.prevent="submit()">
      <div>
        Title: <input type="text" v-model="newPostTitle">
      </div>

      <div>
        Body: <input type="text" v-model="newPostBody">
      </div>

      <div>
        Image: <input type="text" v-model="newPostImage">
      </div>

  </div>
</template>

<style>
</style>

<script>
var axios = require("axios");

export default {
  data: function() {
    return {
      errors: [],
      newPostTitle: "",
      newPostBody: "",
      newPostImage: ""
    };
  },
  created: function() {},
  methods: {
    submit: function() {
      var clientParams = {
        title: this.newPostTitle,
        body: this.newPostBody,
        image: this.newPostImage
      };

      axios
        .post("/api/posts", clientParams)
        .then(response => {
          this.$router.push("/");
        })
        .catch(error => {
          this.errors = error.response.data.errors; 
        });
    }
  }
}; 
</script>


