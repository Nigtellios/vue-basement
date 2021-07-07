<!-- This component is downloading Selected data from parent and rendering "Cart" -->

<template>
  <aside class="product__sidebar" v-if="renderFeatures">
    <span
        class="product__sidebar-counter"
        v-if="featureCounter > 0"
    >
      {{ featureCounter }}
    </span>
    <div
        class="product__sidebar-variant"
        v-if="selectedVariant"
        v-for="(variant, index) in selectedVariant"
        :key="selectedVariant.variantID"
    >
      <img
          class="product__sidebar-variant-img"
          :src="`${variant.variantImage}`"
          :alt="`${variant.variantImage}`"
      >
      <div class="product__sidebar-variant-content">
        <p class="product__sidebar-variant-name">
          {{ variant.variantColor }}
        </p>
        <a
           class="product__sidebar-variant-btn-close"
           @click="deleteSelectedVariant(variant)"
        >
          X
        </a>
      </div>
    </div>

    <div class="active-list">
      <div
          class="active-list__item"
          v-for="activeHighlight in activeHighlights"
          :key="activeHighlight.highlightID"
      >
        <div class="active-list__item-image-box">
          <img
              :src="`${ activeHighlight.highlightImage }`"
              :alt="`${ activeHighlight.highlightImageAlt}`"
          />
        </div>
        <div class="active-list__item-content">
          <h5>
            {{ activeHighlight.highlightTitle }}
          </h5>
        </div>
        <a
            class="active-list__item-delete-btn"
            @click="deleteFeatureFromCart(activeHighlight)"
        >
          X
        </a>
      </div>
    </div>

    <a
        class="product__sidebar-close"
        @click="toggleSidebar"
    >
      CLOSE
    </a>
  </aside>
</template>

<script>
export default {
  name: 'Sidebar',
  props: {
    /* Data */
    renderFeatures: {
      type: Number,
      required: true
    },
    selectedVariant: {
      type: Array,
      required: true
    },
    activeHighlights: {
      type: Array,
      required: true
    },

    /* Computed */
    featureCounter: {
      required: true
    },
  },
  methods: {
    toggleSidebar() {
      this.$emit('toggleSidebar');
    },
    deleteFeatureFromCart(highlight) {
      this.$emit('deleteFeatureFromCart', highlight);
    },
    deleteSelectedVariant(variant) {
      this.$emit('deleteSelectedVariant', variant);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./Sidebar.scss" />