<template>
  <div class="product">

    <section class="product__hero">
      <div class="product__column">
        <img class="product__image" :src="`${productImage}`" alt="Picture of Tesla Model X" />
      </div>
      <div class="product__column">
        <h1 class="product__heading">{{ productName }}</h1>
        <p class="product__under-tag">{{ productUnderTag }}</p>
        <div class="product__column-description-box">
          <p class="product__description">{{ productDescription }}</p>
          <p class="product__description">Order availability status:</p>
          <span v-if="stockAmount > 10" class="availability available">Available!</span>
          <span v-else-if="stockAmount <= 10 && stockAmount > 0" class="availability hurry-up">Hurry up!</span>
          <span v-else class="availability unavailable">Currently unavailable!</span>
          <a :href="productCtaLink" target="_blank"><p class="product__description-cta">{{ productCtaHeading }}</p></a>
        </div>
      </div>
    </section>

    <section class="product__features">
      <div class="product__features-item" v-for="feature in featuresData" :key="feature.featureID">
        <img :src="`${feature.iconURL}`" alt=""/>
        <h4>{{ feature.featureName }}</h4>
        <p>{{ feature.featureDescription }}</p>
      </div>
    </section>

    <section class="product__highlights">
    </section>

  </div>
</template>

<script>
export default {
  name: 'SingleProductPageVue2',
  props: {
  },
  data() {
    return {
      productName: 'Tesla Model X',
      productUnderTag: 'Plaid',
      productDescription: 'Long Range and Plaid platforms unite powertrain and battery technologies for unrivaled performance, range and efficiency. New module and pack thermal architecture allows faster charging and gives you more power and endurance in all conditions.',
      productImage: '../../assets/img/tesla-model-x-on-road.jpeg',
      productImageAlt: 'Tesla Model X on The Road',
      productCtaHeading: 'Check more at Tesla website!',
      productCtaLink: 'https://www.tesla.com/modelx',
      stockAmount: 8,
      featuresData: [
          {
            "featureID": "0",
            "iconURL": "/",
            "featureName": "Range",
            "featureDescription": "340 Miles"
          },
          {
            "featureID": "1",
            "iconURL": "/",
            "featureName": "2,5s",
            "featureDescription": "0-60 mph*"
          },
          {
            "featureID": "2",
            "iconURL": "/",
            "featureName": "9.9s",
            "featureDescription": "1/4 Mile"
          },
          {
            "featureID": "3",
            "iconURL": "/",
            "featureName": "1,020hp",
            "featureDescription": "Peak Power"
          }
      ]
    }
  },
  methods: {
    // Webpack asset parsing workaround
    /* getPictureURL(picture) {
       return require('../../assets/img/' + picture)
     },
     getIconURL(icon) {
       return require('../../assets/icons/' + icon.iconURL)
     }, */
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./SingleProductPageVue2.scss" />
