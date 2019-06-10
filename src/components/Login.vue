<template>
  <div id="login">
    <router-link to="/">Home</router-link>
    <input type="text" v-model="username" placeholder="아이디">
    <input type="password" v-model="password" placeholder="비밀번호">
    <button type="button" v-on:click="login">로그인</button>
    <router-link to="/register">회원가입</router-link>
  </div>
</template>

<script>
import axios from 'axios'
import { mapState } from 'vuex'

export default {
  name: 'Login',
  data: function () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    login: function (e) {
      const self = this
      axios.post(self.apiUrl + '/api/token/', {
        username: self.username,
        password: self.password
      }).then(function (response) {
        console.log(response)
        self.$cookie.set('refreshToken', response.data.refresh, 7)
        self.$router.push('/')
      }).catch(function (error) {
        console.log(error)
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
