<template>
  <div id="main">
    <button type="button">로그아웃</button>
    <button type="button">글작성</button>
    <select class="post-type-select">
      <option value="sell">팔기</option>
      <option value="buy">사기</option>
    </select>
    <PostCard v-for="post in posts" :key="post.id" :post-title="post.title" :post-id="post.id" :price="post.price"></PostCard>
  </div>
</template>

<script>
import PostCard from '@/components/PostCard.vue'
import { mapState, mapActions } from 'vuex'
import axios from 'axios'

export default {
  name: 'Main',
  components: {
    PostCard
  },
  data: function () {
    return {
      posts: []
    }
  },
  created: function () {
    const refreshToken = this.$cookie.get('refreshToken')

    if (refreshToken === null) {
      this.$router.push('/login')
    }
    this.getAccessToken(refreshToken)

  },
  methods: {
    ...mapActions([
      'getAccessToken'
    ])
  },
  computed: {
    ...mapState({
      apiUrl: 'apiUrl',
      accessToken: 'accessToken'
    })
  },
  watch: {
    accessToken: function (newAccessToken) {
      const self = this
      axios.get(this.apiUrl + '/api/posts/', {
        headers: {
          Authorization: 'Bearer ' + this.accessToken
        }
      }).then(function (response) {
        self.posts = response.data
      })
    }
  }
}
</script>

<style scoped>

</style>
