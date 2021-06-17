<template>
  <div class="hello">
    <h3>Hello There {{ msg }}</h3>
  </div>
</template>

<script>
export default {
  name: 'MainScreenVue2',
  props: {
    msg: String
  },
  data() {
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./MainScreenVue2.scss" />
