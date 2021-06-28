<template>
  <div class="product">

    <section class="product__hero">
      <div class="product__column">
        <div class="product__column-transition-box">
          <transition name="fade" mode="out-in">
            <img class="product__image" :src="`${variantImage}`" :alt="`${variantImageAlt}`" :key="variantImage" />
          </transition>
        </div>
      </div>
      <div class="product__column">
        <h1 class="product__heading">{{ productName }}</h1>
        <p class="product__under-tag">{{ productUnderTag }}</p>
        <div class="product__column-description-box">
          <p class="product__description">{{ productDescription }}</p>
          <p class="product__description">Order availability status:</p>

          <div v-if="inStock >= stockAlerts.minimumAvailable" class="availability available">
            <p>Available!</p>
          </div>
          <div v-else-if="inStock <= stockAlerts.low && inStock > stockAlerts.unavailable" class="availability hurry-up">
            <p>Hurry up!</p>
          </div>
          <div v-else class="availability unavailable">
            <p>Currently unavailable!</p>
          </div>

          <div class="variants">
            <div class="variants__item" @mouseover="updateProduct(index)" @click="selectVariant(variant)" v-for="(variant, index) in carVariants" :key="carVariants.variantID">
              <div class="variants__item-icon" :style="{ background: variant.variantColorCode }"></div>
              <div class="variants__item-heading">{{ variant.variantColor }}</div>
            </div>
          </div>

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
            <a class="product__highlights-btn" @click="addFeatureToCart(highlight)"><p class="cta">Add this feature</p></a>
          </div>
        </div>
      </div>
    </section>

    <transition name="fade">
      <aside class="product__sidebar" v-if="renderFeatures">
        <span class="product__sidebar-counter" v-if="featureCounter > 0">{{ featureCounter }}</span>

        <div class="product__sidebar-variant" v-if="selectedVariant" v-for="(variant, index) in selectedVariant" :key="selectedVariant.variantID">
          <img class="product__sidebar-variant-img" :src="`${variant.variantImage}`" :alt="`${variant.variantImage}`">
          <div class="product__sidebar-variant-content">
            <p class="product__sidebar-variant-name">{{ variant.variantColor }}</p>
            <a class="product__sidebar-variant-btn-close" @click="deleteSelectedVariant(variant)">X</a>
          </div>
        </div>

        <div class="active-list">
          <div class="active-list__item" v-for="activeHighlight in activeHighlights" :key="activeHighlight.highlightID">
            <div class="active-list__item-image-box">
              <img :src="`${ activeHighlight.highlightImage }`" :alt="`${ activeHighlight.highlightImageAlt}`"/>
            </div>
            <div class="active-list__item-content">
              <h5>{{ activeHighlight.highlightTitle }}</h5>
            </div>
            <a class="active-list__item-delete-btn" @click="deleteFeatureFromCart(activeHighlight)">X</a>
          </div>
        </div>

        <a class="product__sidebar-close" @click="toggleSidebar">CLOSE</a>
    </aside>
    </transition>

    <transition name="slide">
      <div class="product__modal-bcg" v-if="renderFeatures" @click="toggleSidebar"></div>
    </transition>

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
      productCtaHeading: 'Check more at Tesla website!',
      productCtaLink: 'https://www.tesla.com/modelx',
      renderFeatures: false,
      carVariants: [
        {
          "variantID": 0,
          "variantColor": "White",
          "variantColorCode": "#F7F7F7",
          "variantImage": "../../assets/img/tesla-x-white.jpg",
          "variantImageAlt": "White Tesla Model X",
          "variantQuantity": 5
        },
        {
          "variantID": 1,
          "variantColor": "Silver",
          "variantColorCode": "#717171",
          "variantImage": "../../assets/img/tesla-x-silver.jpg",
          "variantImageAlt": "Silver Tesla Model X",
          "variantQuantity": 0
        },
        {
          "variantID": 2,
          "variantColor": "Blue",
          "variantColorCode": "#0D47AC",
          "variantImage": "../../assets/img/tesla-x-blue.jpg",
          "variantImageAlt": "Blue Tesla Model X",
          "variantQuantity": 6
        },
        {
          "variantID": 4,
          "variantColor": "Red",
          "variantColorCode": "#CF0001",
          "variantImage": "../../assets/img/tesla-x-red.jpg",
          "variantImageAlt": "Red Tesla Model X",
          "variantQuantity": 1
        },
        {
          "variantID": 5,
          "variantColor": "Black",
          "variantColorCode": "#000000",
          "variantImage": "../../assets/img/tesla-x-black.jpg",
          "variantImageAlt": "Black Tesla Model X",
          "variantQuantity": 10
        },
      ],
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
      stockAlerts: {
        'unavailable': 0,
        'low': 5,
        'minimumAvailable': 5
      },
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
      ],
      selectedVariant: [],
      selectedVariantID: 0,
      activeHighlights: [],
    }
  },
  methods: {
    // Add Highlighted Feature to Cart
    // Close/Open Cart (Sidebar)
    toggleSidebar () {
      this.renderFeatures = !this.renderFeatures;
    },

    addFeatureToCart (highlight) {

      this.toggleSidebar();

      if (this.activeHighlights.some((item) => item.highlightID === highlight.highlightID)) {
        return alert(`You've already added „${highlight.highlightTitle}"!`);
      } else {
        this.activeHighlights.push(highlight);
      }
    },

    // Delete Highlighted Feature from Cart
    deleteFeatureFromCart (highlight) {
      let indexOf = this.activeHighlights.indexOf(highlight);

      if (this.activeHighlights.some((item) => item.highlightID === highlight.highlightID)) {
        this.activeHighlights.splice(indexOf, 1);
      } else {
        alert(`Item with ID ${highlight.highlightID} does not exist!`);
      }
    },

    updateProduct(index) {
      this.selectedVariantID = index;
    },

    // Select & Pass Variant to Cart
    selectVariant(variant) {
      this.toggleSidebar();
      if (this.selectedVariant.some((item) => item.variantID === variant.variantID)) {
        return alert(`Car with color ${variant.variantColor} is already in Cart!`);
      } else if (this.selectedVariant.length >= 1) {
        return alert(`You can select only one variant per order!`);
      } else if (variant.variantQuantity <= 0) {
        this.renderFeatures = false;
        return alert(`We're sorry, this variant is out of stock.`);
      } else {
        this.selectedVariant.push(variant);
        console.log(this.selectedVariant.variantQuantity)
      }
    },

    // Delete Selected Variant from Card
    deleteSelectedVariant(variant) {
      let indexOf = this.selectedVariant.indexOf(variant);
      if (this.selectedVariant.some((item) => item.variantID === variant.variantID)) {
        this.selectedVariant.splice(indexOf, 1);
      } else {
        alert(`Item with ID ${variant.variantID} does not exist!`);
      }
    }

    // Webpack asset parsing workaround - If they are not in /public/
    /* getPictureURL(picture) {
       return require('../../assets/img/' + picture)
     },
     getIconURL(icon) {
       return require('../../assets/icons/' + icon.iconURL)
     }, */
  },
  computed: {
    featureCounter() {
      return this.activeHighlights.length;
    },
    variantImage() {
      return this.carVariants[this.selectedVariantID].variantImage;
    },
    variantImageAlt() {
      return this.carVariants[this.selectedVariantID].variantImageAlt;
    },
    inStock() {
      return this.carVariants[this.selectedVariantID].variantQuantity;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./SingleProductPageVue2.scss" />
