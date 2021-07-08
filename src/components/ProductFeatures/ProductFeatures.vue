<template>
  <section class="features">
    <div
        class="features__item"
        v-for="feature in productFeaturesData"
        :key="feature.featureID"
    >
      <img
          class="features__icon"
          :src="`${feature.iconURL}`"
          :alt="`${feature.iconAlt}`"
      />
      <div class="features__content">
        <h4 class="features__heading">
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