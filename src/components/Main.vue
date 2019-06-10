<template>
  <div id="main">
    <button type="button" v-on:click="logout">로그아웃</button>
    <button type="button" v-on:click="goToWritePost">글작성</button>
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
      posts: [],
      accessToken: ''
    }
  },

  created: function () {
    const refreshToken = this.$cookie.get('refreshToken')

    if (refreshToken === null) {
      this.$router.push('/login')
    }

    const self = this
    axios.post(this.apiUrl + '/api/token/refresh/', {
      refresh: refreshToken
    }).then(function (response) {
      self.$cookie.set('access', response.data.access, 1)
      self.accessToken = response.data.access
    }).catch(function (error) {
      self.$cookie.delete('refresh')
      self.$router.push('/login')
    })
  },

  computed: {
    ...mapState({
      apiUrl: 'apiUrl'
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
  },

  methods: {
    logout: function () {
      this.$cookie.delete('refreshToken')
      this.$cookie.delete('access')
      this.$router.push('/login')
    },

    goToWritePost: function () {
      this.$router.push('post-add')
    }
  }
}
</script>

<style scoped>

</style>
