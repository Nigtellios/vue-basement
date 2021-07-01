<template>
  <section class="product__hero">
    <div class="product__column">
      <div class="product__column-transition-box">
        <transition name="fade" mode="out-in">
          <img class="product__image" :src="`${image}`" :alt="`${imageAlt}`" :key="image" />
        </transition>
      </div>
    </div>
    <div class="product__column">
      <h1 class="product__heading">{{ productName }}</h1>
      <p class="product__under-tag">{{ productUnderTag }}</p>
      <div class="product__column-description-box">
        <p class="product__description">{{ productDescription }}</p>
        <p class="product__description">Order availability status:</p>

        <div v-if="isInStock >= stockAlerts.minimumAvailable" class="availability available">
          <p>Available!</p>
        </div>
        <div v-else-if="isInStock <= stockAlerts.low && isInStock > stockAlerts.unavailable" class="availability hurry-up">
          <p>Hurry up!</p>
        </div>
        <div v-else class="availability unavailable">
          <p>Currently unavailable!</p>
        </div>

        <div class="variants">
          <div class="variants__item" @mouseover="update(index)" @click="select(variant)" v-for="(variant, index) in carVariants" :key="carVariants.variantID">
            <div class="variants__item-icon" :style="{ background: variant.variantColorCode }"></div>
            <div class="variants__item-heading">{{ variant.variantColor }}</div>
          </div>
        </div>

        <a :href="productCtaLink" target="_blank"><p class="product__description-cta">{{ productCtaHeading }}</p></a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductHeroVue2',
  props: {
    /* Data */
    productName: {
      type: String,
      required: true,
    },
    productUnderTag: {
      type: String,
      required: true,
    },
    productDescription: {
      type: String,
      required: true,
    },
    productCtaHeading: {
      type: String,
      required: false,
    },
    productCtaLink: {
      type: String,
      required: false,
    },
    renderFeatures: {
      type: Boolean,
      required: true
    },
    carVariants: {
      type: Array,
      required: true
    },
    stockAlerts: {
      type: Object,
      required: true,
    },
    selectedVariant: {
      type: Array,
      required: true
    },
    variantImage: {
      required: true
    },
    variantImageAlt: {
      required: true
    },
    inStock: {
      required: true
    },
  },
  data() {

  },
  methods: {
    update(index){
      this.$emit('updateProduct', index);
      console.log('EMITED');
    },
    select(variant){
      this.$emit('selectVariant', variant);
      console.log('EMITED');
    },
  },
  computed: {
    image() {
      this.$emit('variantImage');
    },
    imageAlt() {
      this.$emit('variantImageAlt') ;
    },
    isInStock() {
      this.$emit('inStock');
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductHeroVue2.scss" />