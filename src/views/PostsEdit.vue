<template>
  <div class="posts-edit">
    <h1>Edit Post</h1>
    <ul>
      <li v-for="error in errors">{{ error }}</li>
    </ul>

    <form v-on:submit.prevent="submit()">
      <div>
        Title: <input type="text" v-model="post.title">
      </div>

      <div>
        Body: <input type="text" v-model="post.body">
      </div>

      <div>
        Image: <input type="text" v-model="post.image">
      </div>

      <input type="submit" name="Update">
    </form>
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
      post: {}
    }; 
  }, 
  created: function() {
    axios
      .get("/api/posts/" + this.$route.params.id)
      .then(response => {
        this.recipe = response.data; 
      }); 
  },
  methods: {
    submit: function() {
      var clientParams = this.post;

      axios
        .patch("/api/posts/" + this.$route.params.id, clientParams)
        .then(response => {
          this.$router.push("/posts/" + response.data.id);
        })
        .catch(error => {
          this.errors = error.response.data.errors; 
        }); 
    }
  }
}; 

</script>