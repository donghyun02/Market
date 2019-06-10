<template>
  <div id="register">
    <input type="text" v-model="username" placeholder="아이디">
    <input type="password" v-model="password" placeholder="비밀번호">
    <button type="button" name="button" v-on:click="register">회원가입</button>
    <router-link to="login">로그인</router-link>
  </div>
</template>

<script>
import axios from 'axios'
import { mapState } from 'vuex'

export default {
  name: 'Register',
  data: function () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    register: function (e) {
      if (this.username === '' || this.password === '') {
        alert('값을 모두 입력해주세요.')
      }
      else {
        const self = this
        axios.post(self.apiUrl + '/accounts/register/', {
          username: self.username,
          password: self.password
        }).then(function (response) {
          if (response.status == 201) {
            self.$router.push('/login')
          }
        }).catch(function (error) {
          alert('존재하는 계정입니다.')
        })
      }
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
