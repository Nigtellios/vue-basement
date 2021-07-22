<!-- This component is downloading Selected data from parent and rendering "Cart" -->

<template>
  <aside class="sidebar" v-if="renderFeatures">
    <span
        class="sidebar__counter"
        v-if="featureCounter > 0"
    >
      {{ featureCounter }}
    </span>
    <div
        class="sidebar__variant"
        v-for="(variant, index) in selectedVariant"
        :key="selectedVariant.variantID"
    >
      <div v-if="selectedVariant">
        <img
            class="sidebar__variant-img"
            :src="`${variant.variantImage}`"
            :alt="`${variant.variantImage}`"
        >
        <div class="sidebar__variant-content">
          <p class="sidebar__variant-name">
            {{ variant.variantColor }}
          </p>
          <a
              class="sidebar__variant-btn-close"
              @click="deleteSelectedVariant(variant)"
          >
            X
          </a>
        </div>
      </div>
    </div>

    <div class="sidebar__active-list">
      <div
          class="sidebar__active-list-item"
          v-for="activeHighlight in activeHighlights"
          :key="activeHighlight.highlightID"
      >
        <div class="sidebar__active-list-item-image-box">
          <img
              :src="`${ activeHighlight.highlightImage }`"
              :alt="`${ activeHighlight.highlightImageAlt}`"
          />
        </div>
        <div class="sidebar__active-list-item-content">
          <h5>
            {{ activeHighlight.highlightTitle }}
          </h5>
        </div>
        <a
            class="sidebar__active-list-item-delete-btn"
            @click="deleteFeatureFromCart(activeHighlight)"
        >
          X
        </a>
      </div>
    </div>

    <a
        class="sidebar__close"
        @click="toggleSidebar"
    >
      CLOSE
    </a>
  </aside>
</template>

<script>
export default {
  name: 'ProductSidebar',
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
<style lang="scss" src="./ProductSidebar.scss" />