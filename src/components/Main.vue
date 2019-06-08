<template>
  <div id="main">
    <button type="button">로그인</button>
    <select class="post-type-select">
      <option value="sell">팔기</option>
      <option value="buy">사기</option>
    </select>
    <PostCard />
    <PostCard />
    <PostCard />
  </div>
</template>

<script>
import PostCard from '@/components/PostCard.vue'

export default {
  name: 'Main',
  components: {
    PostCard
  }
}
</script>

<style scoped>

</style>
