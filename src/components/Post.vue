<template>
  <div>
    <h4>
      <input :disabled="post.disabled" @blur="updatePost" v-model="post.title" />
      <span v-if="post.id">
        -
        <i @click="post.disabled = !post.disabled" class="far fa-edit"></i> -
        <i @click="deletePost" class="fas fa-trash-alt"></i>
      </span>
    </h4>
    <textarea rows="8" cols="30" @blur="updatePost" :disabled="post.disabled" v-model="post.body" />
  </div>
</template>

<script>
export default {
  name: "postItem",
  props: ["post"],
  data() {
    return {};
  },
  methods: {
    updatePost() {
      if (this.post.id) {
        this.post.disabled = true;
      }
    },
    deletePost() {
      this.$emit("deletePost", this.post.id);
    }
  }
};
</script>

<style>
</style>
