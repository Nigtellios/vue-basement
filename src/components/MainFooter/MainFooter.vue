<template>
  <footer class="footer">
    <div class="footer__copyright">
      <div class="footer__copyright-info">
        <p class="footer--p">
          Training Website. All rights belongs to
          <a
              class="footer--hyper"
              href="https://www.tesla.com/"
              target="_blank"
          >
            TESLA.
          </a>
        </p>
      </div>
      <div class="footer__copyright-created">
        <p class="footer--p">
          {{ currentDate() }}, made with
          <span class="love">love</span>
          by
          <a
              class="footer--hyper"
              href="https://jakubkowalski.dev/"
              target="_blank"
          >
            jakubkowalski.dev
          </a>
        </p>
      </div>
    </div>
  </footer>
</template>

<script>
export default {
  name: 'MainFooter',
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