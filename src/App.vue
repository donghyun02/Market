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
