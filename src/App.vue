<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
import Vue from 'vue'
import Vuex from 'vuex'
import VueCookie from 'vue-cookie'
import axios from 'axios'

Vue.use(Vuex)
Vue.use(VueCookie)

const store = new Vuex.Store({
  state: {
    apiUrl: 'http://localhost:8000',
    accessToken: ''
  },
  mutations: {
    setAccessToken (state, payload) {
      state.accessToken = payload.accessToken
    }
  },
  actions: {
    getAccessToken (context, refreshToken) {
      const self = this
      axios.post(context.state.apiUrl + '/api/token/refresh/', {
        refresh: refreshToken
      }).then(function (response) {
        context.commit('setAccessToken', {
          accessToken: response.data.access
        })
      }).catch(function (error) {
        self.$cookie.delete('refresh')
        self.$router.push('/login')
      })
    }
  }
})

export default {
  name: 'app',
  store
}
</script>

<style>
#app {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}
</style>
