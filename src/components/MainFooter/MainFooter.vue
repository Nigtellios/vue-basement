<template>
  <footer class="footer">
    <div class="footer__copyright">
      <div class="footer__copyright-info">
        <p>All rights belongs to TESLA.</p>
      </div>
      <div class="footer__copyright-created">
        <p>{{ currentDate() }}</p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'MainFooter',
  props: {

  },
  methods: {
    currentDate() {
      const date = new Date();
      return date.getFullYear();
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./MainFooter.scss" />