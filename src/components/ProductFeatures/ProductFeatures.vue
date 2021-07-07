<template>
  <section class="product__features">
    <div
        class="product__features-item"
        v-for="feature in productFeaturesData"
        :key="feature.featureID"
    >
      <img
          class="product__features-icon"
          :src="`${feature.iconURL}`"
          :alt="`${feature.iconAlt}`"
      />
      <div class="product__features-content">
        <h4 class="product__features-heading">
          {{ feature.featureName }}
        </h4>
        <p>
          {{ feature.featureDescription }}
        </p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductFeatures',
  props: {
    productFeaturesData: {
      type: Array,
      required: true
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductFeatures.scss" />