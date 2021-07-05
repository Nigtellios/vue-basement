<template>
  <section class="product__highlights">
    <div class="product__highlights-row" v-for="highlight in highlightsData" :key="highlight.highlightID">
      <div class="product__highlights-column">
        <img class="product__highlights-image" :src="`${highlight.highlightImage}`" :alt="`${highlight.highlightImageAlt}`"/>
      </div>
      <div class="product__highlights-column">
        <div class="product__highlights-content">
          <h5 class="product__highlights-heading">{{ highlight.highlightTitle }}</h5>
          <p class="product__highlights-p">{{ highlight.highlightDescription }}</p>
          <a class="product__highlights-btn" @click="addFeatureToCart(highlight)"><p class="cta">Add this feature</p></a>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductHighlightsVue2',
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
<style lang="scss" src="./ProductHighlightsVue2.scss" />