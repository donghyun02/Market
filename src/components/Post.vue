<template>
  <div id="post">
    <router-link to="/">Home</router-link>
    <p>{{ title }}</p>
    <p>{{ author }}</p>
    <p>{{ price }}</p>
    <p>{{ content }}</p>
    <input type="text" v-model="comment" placeholder="comment">
    <button type="button" name="button" v-on:click="submitComment">submit</button>
    <p>comments</p>
    <CommentCard v-for="comment in comments" :key="comment.id" :content="comment.content" :name="comment.nickname"></CommentCard>
  </div>
</template>

<script>
import CommentCard from '@/components/CommentCard.vue'
import { mapState } from 'vuex'
import axios from 'axios'

export default {
  name: 'Post',
  components: {
    CommentCard
  },
  data: function () {
    return {
      title: '',
      price: null,
      content: '',
      author: null,
      comment: '',
      comments: []
    }
  },
  created: function () {
    const self = this
    axios.get(this.apiUrl + '/api/post/' + this.$route.params.postId, {
      headers: {
        Authorization: 'Bearer ' + this.accessToken
      }
    }).then(function (response) {
      console.log(response.data)
      const data = response.data
      self.title = data.title
      self.price = data.price
      self.content = data.content
      self.author = data.author.username
      self.comments = data.comments
    })
  },
  methods: {
    submitComment: function () {
      axios.post(this.apiUrl + '/api/comments/', {
        post_id: this.$route.params.postId,
        content: this.comment
      }, {
        headers: {
          Authorization: 'Bearer ' + this.accessToken
        }
      }).then(function (response) {
        console.log(response)
      })
    }
  },
  computed: {
    ...mapState({
      apiUrl: 'apiUrl',
      accessToken: 'accessToken'
    })
  }
}
</script>

<style scoped>

</style>
