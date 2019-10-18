<template>
  <div id="app">
    <div class="container">
      <div class="row col-sm-12 mb-3">
        <div class="col-sm-4">
          <button class="btn btn-primary" @click="resetNewPost">New Post</button>
        </div>
        <div v-if="showNewPost" class="col-sm-8" id="form-input">
          New Post
          <post :post="newPost" />
          <button class="btn btn-success mt-4 mr-2" @click="addNewPost">Submit</button>
          <button class="btn btn-danger mt-4" @click="resetNewPost">Cancel</button>
        </div>
      </div>
      
      <div class="row col-sm-12 mt-4">
        <div class="col-sm-4 mb-3" v-bind:key="post.id" v-for="post in posts">
          <post :post="post" @deletePost="deletePost" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Post from "./Post.vue";

export default {
  name: "app",
  components: {
    Post
  },
  mounted() {
    axios.get("https://jsonplaceholder.typicode.com/posts").then(res => {
      this.posts = res.data.map(post => ({ ...post, disabled: true })); //spread operator
    });
  },
  data() {
    return {
      posts: [],
      newPost: {
        userId: "",
        title: "",
        body: ""
      },
      showNewPost: false
    };
  },
  methods: {
    addNewPost() {
      this.newPost.disabled = true;
      this.newPost.id = this.posts.length + 1;
      this.posts.unshift(this.newPost);
      this.resetNewPost();
    },
    resetNewPost() {
      this.newPost = {};
      this.showNewPost = !this.showNewPost;
    },
    deletePost(id) {
      this.posts = this.posts.filter(post => post.id !== id);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
#form-input{
  max-width: 575px;
}

@media screen and (max-width: 575px){
  #app{
    text-align: center;
  }
  #form-input{
    text-align: center;
    margin-top: 30px;
  }
}
</style>
