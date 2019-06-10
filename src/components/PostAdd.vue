<template>
  <div id="post-add">
    <router-link to="/">Home</router-link>
    <input type="text" v-model="title" placeholder="title">
    <input type="text" v-model="content" placeholder="content">
    <input type="text" v-model="price" placeholder="price">
    <button type="button" v-on:click="submit">작성하기</button>
  </div>
</template>

<script>
import axios from 'axios'
import { mapState } from 'vuex'

export default {
  name: 'PostAdd',

  data: function () {
    return {
      title: '',
      content: '',
      price: null,
      accessToken: ''
    }
  },

  created: function () {
    const access = this.$cookie.get('access')
    if (access === null) {
      this.$router.push('/login')
    }
    this.accessToken = access
  },

  methods: {
    submit: function () {
      const self = this
      axios.post(this.apiUrl + '/api/posts/', {
        title: this.title,
        content: this.content,
        price: Number(this.price)
      }, {
        headers: {
          Authorization: 'Bearer ' + this.accessToken
        }
      }).then(function () {
        self.$router.push('/')
      })
    }
  },

  computed: {
    ...mapState({
      apiUrl: 'apiUrl'
    })
  }
}
</script>

<style scoped>
</style>
