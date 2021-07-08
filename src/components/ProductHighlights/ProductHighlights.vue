<template>
  <section class="highlights">
    <div
        class="highlights__row"
        v-for="highlight in highlightsData"
        :key="highlight.highlightID"
    >
      <div class="highlights__column">
        <img
            class="highlights__image"
            :src="`${highlight.highlightImage}`"
            :alt="`${highlight.highlightImageAlt}`"
        />
      </div>
      <div class="highlights__column">
        <div class="highlights__content">
          <h5 class="highlights__heading">
            {{ highlight.highlightTitle }}
          </h5>
          <p class="highlights__p">
            {{ highlight.highlightDescription }}
          </p>
          <a
              class="highlights__btn"
              @click="addFeatureToCart(highlight)"
          >
            <p class="cta">
              Add this feature
            </p>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductHighlights',
  props: {
    /* Data */
    highlightsData: {
      type: Array,
      required: true
    },
    activeHighlights: {
      type: Array,
      required: true
    },
  },
  methods: {
    addFeatureToCart(highlight) {
      this.$emit('add-feature-to-cart', highlight);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductHighlights.scss" />