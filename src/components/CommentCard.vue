<template>
  <div id="comment-card">
    <span>{{ content }}</span>
    <span>{{ name }}</span>
  </div>
</template>

<script>
export default {
  name: 'CommentCard',
  props: {
    content: {
      required: true,
      type: String
    },
    name: {
      required: true,
      type: String
    }
  }
}
</script>

<style scoped>
</style>
