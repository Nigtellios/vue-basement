<template>
  <section id="info" class="info">
    <div class="info__column">
      <div class="info__column-transition-box">
        <transition name="fade" mode="out-in">
          <img
              class="info__image"
              :src="variantImage"
              :alt="variantImageAlt"
              :key="variantImage"
          />
        </transition>
      </div>
    </div>
    <div class="info__column">
      <h1 class="info__heading">
        {{ productName }}
      </h1>
      <p class="info__under-tag">
        {{ productUnderTag }}
      </p>
      <div class="info__column-description-box">
        <p class="info__description">
          {{ productDescription }}
        </p>
        <p class="info__description">
          Order availability status:
        </p>
        <div v-if="inStock >= stockAlerts.minimumAvailable" class="availability available">
          <p>
            Available!
          </p>
        </div>
        <div
            v-else-if="inStock <= stockAlerts.low && inStock > stockAlerts.unavailable"
            class="availability hurry-up"
        >
          <p>
            Hurry up!
          </p>
        </div>
        <div v-else class="availability unavailable">
          <p>
            Currently unavailable!
          </p>
        </div>

        <div class="variants">
          <div 
            class="variants__item"
            @mouseover="updateProduct(index)"
            @click="selectVariant(variant)" 
            v-for="(variant, index) in carVariants" 
            :key="variant.variantID"
          >
            <div
                class="variants__item-icon"
                :style="{ background: variant.variantColorCode }"
            ></div>
            <div class="variants__item-heading">
              {{ variant.variantColor }}
            </div>
          </div>
        </div>

        <a :href="productCtaLink" target="_blank">
          <p class="product__description-cta">
            {{ productCtaHeading }}
          </p>
        </a>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductInfo',
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
      type: Object,
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

    /* Computed */
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
    return {

    }
  },
  methods: {
    updateProduct(index){
      this.$emit('updateProduct', index);
      //console.log("Index Value: " + index);
      //console.log("Selected Variant ID: " + this.selectedVariantID);
    },
    selectVariant(variant){
      this.$emit('selectVariant', variant);
      console.log("Selected Variant Object: " + variant);
    },
  },
  computed: {

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductInfo.scss" />