<template>
  <div class="product">

    <product-hero-vue2
        :product-name="productName"
        :product-under-tag="productUnderTag"
        :product-description="productDescription"
        :render-features="renderFeatures"
        :car-variants="carVariants"
        :stock-alerts="stockAlerts"
        :selected-variant="selectedVariant"
        :in-stock="inStock"
        :variant-image="variantImage"
        :variant-image-alt="variantImageAlt"
        @updateProduct="updateProduct"
        @selectVariant="selectVariant"
    />

    <product-features-vue2
        :product-features-data="productFeaturesData"
    />

    <product-highlights-vue2
        :highlights-data="highlightsData"
        :active-highlights="activeHighlights"
        @addFeatureToCart="addFeatureToCart"
    />

    <transition name="fade">
      <SidebarVue2
          :render-features="renderFeatures"
          :active-highlights="activeHighlights"
          :selected-variant="selectedVariant"
          :feature-counter="featureCounter"
          @toggleSidebar="toggleSidebar"
          @deleteFeatureFromCart="deleteFeatureFromCart"
          @deleteSelectedVariant="deleteSelectedVariant"
      />
    </transition>

    <transition name="slide">
      <div
          class="product__modal-bcg"
          v-if="renderFeatures"
          @click="toggleSidebar"
      ></div>
    </transition>

  </div>
</template>

<script>
import ProductHeroVue2 from "@/components/ProductHeroVue2/ProductHeroVue2";
import ProductFeaturesVue2 from "@/components/ProductFeaturesVue2/ProductFeaturesVue2";
import ProductHighlightsVue2 from "@/components/ProductHighlightsVue2/ProductHighlightsVue2";
import SidebarVue2 from "@/components/SidebarVue2/SidebarVue2";

export default {
  name: 'SingleProductPageVue2',
  components: {
    SidebarVue2,
    ProductHeroVue2,
    ProductFeaturesVue2,
    ProductHighlightsVue2,
  },
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
          "variantID": 3,
          "variantColor": "Red",
          "variantColorCode": "#CF0001",
          "variantImage": "../../assets/img/tesla-x-red.jpg",
          "variantImageAlt": "Red Tesla Model X",
          "variantQuantity": 1
        },
        {
          "variantID": 4,
          "variantColor": "Black",
          "variantColorCode": "#000000",
          "variantImage": "../../assets/img/tesla-x-black.jpg",
          "variantImageAlt": "Black Tesla Model X",
          "variantQuantity": 10
        },
      ],
      productFeaturesData: [
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
      activeHighlights: [],
      selectedVariantID: 0,
    }
  },
  methods: {
    // Add Highlighted Feature to Cart
    // Close/Open Cart (Sidebar)
    toggleSidebar() {
      this.renderFeatures = !this.renderFeatures;
    },

    updateProduct(index) {
      console.log(index);
      this.selectedVariantID = index;
    },

    // Select & Pass Variant to Cart
    selectVariant(variant) {
      this.toggleSidebar();
      if (this.selectedVariant.some((item) => item.variantID === variant.variantID)) {
        this.renderFeatures = false;
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

    addFeatureToCart(highlight) {
      this.toggleSidebar();
      if (this.activeHighlights.some((item) => item.highlightID === highlight.highlightID)) {
        return alert(`You've already added „${highlight.highlightTitle}"!`);
      } else {
        this.activeHighlights.push(highlight);
      }
    },

    // Delete Highlighted Feature from Cart
    deleteFeatureFromCart(highlight) {
      let indexOf = this.activeHighlights.indexOf(highlight);

      if (this.activeHighlights.some((item) => item.highlightID === highlight.highlightID)) {
        this.activeHighlights.splice(indexOf, 1);
      } else {
        alert(`Item with ID ${highlight.highlightID} does not exist!`);
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
