<template>
  <div id="post-card">
    <span class="title"><router-link :to="{ name: 'Post', params: { postId: postId } }">{{ postTitle }}</router-link></span>
    <span>{{ price }} </span>
  </div>
</template>

<script>
export default {
  name: 'PostCard',
  
  props: {
    postTitle: {
      required: true,
      type: String
    },
    postId: {
      required: true,
      type: Number
    },
    price: {
      required: true,
      type: Number
    }
  }
}
</script>

<style scoped>

</style>
