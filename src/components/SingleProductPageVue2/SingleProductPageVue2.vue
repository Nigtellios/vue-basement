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
        <img class="product__features-icon" :src="`${feature.iconURL}`" :alt="`${feature.iconAlt}`"/>
        <div class="product__features-content">
          <h4 class="product__features-heading">{{ feature.featureName }}</h4>
          <p>{{ feature.featureDescription }}</p>
        </div>
      </div>
    </section>

    <section class="product__highlights">
      <div class="product__highlights-row" v-for="highlight in highlightsData" :key="highlight.highlightID">
        <div class="product__highlights-column">
          <img class="product__highlights-image" :src="`${highlight.highlightImage}`" :alt="`${highlight.highlightImageAlt}`"/>
        </div>
        <div class="product__highlights-column">
          <div class="product__highlights-content">
            <h5 class="product__highlights-heading">{{ highlight.highlightTitle }}</h5>
            <p class="product__highlights-p">{{ highlight.highlightDescription }}</p>
          </div>
        </div>
      </div>
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
            "iconURL": "../../assets/icons/range.svg",
            "iconAlt": "High range of vehicle",
            "featureName": "Range",
            "featureDescription": "340 Miles"
          },
          {
            "featureID": "1",
            "iconURL": "../../assets/icons/25smph.svg",
            "iconAlt": "in 2.5s from 0 to 60 mph",
            "featureName": "2,5s",
            "featureDescription": "0-60 mph*"
          },
          {
            "featureID": "2",
            "iconURL": "../../assets/icons/14mile.svg",
            "iconAlt": "in 9.9s at 1/4 Mile distance",
            "featureName": "9.9s",
            "featureDescription": "1/4 Mile"
          },
          {
            "featureID": "3",
            "iconURL": "../../assets/icons/peakpower.svg",
            "iconAlt": "1020hp peak power",
            "featureName": "1,020hp",
            "featureDescription": "Peak Power"
          }
      ],
      highlightsData: [
        {
          "highlightID": "0",
          "highlightImage": "../../assets/img/audio-system.jpg",
          "highlightImageAlt": "Best audio system in the market",
          "highlightTitle": "Best Audio System",
          "highlightDescription": "A 22-speaker, 960-watt audio system with active noise canceling offers the best listening experience at home or on the road."
        },
        {
          "highlightID": "1",
          "highlightImage": "../../assets/img/multi-device.jpg",
          "highlightImageAlt": "Stay connected with multiple devices",
          "highlightTitle": "Stay Connected",
          "highlightDescription": "Multi-device Bluetooth, wireless and USB-C charging for every passenger, with enough power to fast-charge your tablets and laptop."
        },
        {
          "highlightID": "2",
          "highlightImage": "../../assets/img/wireless-gaming.jpg",
          "highlightImageAlt": "Let your kids play games while driving",
          "highlightTitle": "Wireless Gaming",
          "highlightDescription": "Up to 10 teraflops of processing power enables in-car gaming on-par with today’s newest consoles. Wireless controller compatibility lets you game from any seat."
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
