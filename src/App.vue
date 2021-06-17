<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <main-screen-vue2 />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import MainScreenVue2 from './components/MainScreenVue2/MainScreenVue2.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    MainScreenVue2
  }
}
</script>
