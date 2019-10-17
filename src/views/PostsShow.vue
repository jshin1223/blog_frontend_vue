<template>
  <div class="posts-show">
    <h1>{{ post.title }}</h1>
    <h5>Body: {{ post.body }}</h5>
    <h4>Image: {{ post.image }}</h4>
    
  </div>
</template>

<style>
</style>

<script>
var axios = require('axios');

export default {
  data: function() {
    return {
      post: {
        id: "",
        title: "",
        body: "",
        image: ""
      }
    };  
  },
  created: function() {
    axios
      .get("/api/posts/" + this.$route.params.id)
      .then(response => {
        this.post = response.data; 
      }); 
  },
  methods: {
    destroyPost: function() {
      axios
        .delete("/api/posts/" + this.post.id)
        .then(response => {
          this.$router.push("/"); 
        });
    }
  }
};
</script>

