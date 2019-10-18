<template>
  <div>
    <h4>
      <div class="edit">
        <div>
          <i @click="post.disabled = !post.disabled" class="far fa-edit fa-1x"></i> -
          <i @click="deletePost" class="fas fa-trash-alt"></i>
        </div>
      </div>
      <input
        :disabled="post.disabled"
        @blur="updatePost"
        v-model="post.title"
        placeholder="Title"
        class="form-control"
      />
      <span v-if="post.id"></span>
    </h4>
    <textarea
      class="form-control"
      placeholder="Body"
      rows="8"
      cols="30"
      @blur="updatePost"
      :disabled="post.disabled"
      v-model="post.body"
    />
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
  .edit{
    display: flex;
    justify-content: flex-end;
  }


</style>
