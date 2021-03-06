<template>
  <div class="product">

    <product-hero
        :product-name="productName"
        :product-excerpt="productExcerpt"
        :product-hero-img="productHeroImg"
        :product-hero-img-alt="productHeroImgAlt"
        :product-hero-cta="productHeroCta"
        :product-hero-cta-scope="productHeroCtaScope"
        :has-box="hasBox"
        :box-color="boxColor"
    />

    <product-info
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

    <product-features
        :product-features-data="productFeaturesData"
    />

    <product-highlights
        :highlights-data="highlightsData"
        :active-highlights="activeHighlights"
        @addFeatureToCart="addFeatureToCart"
    />

    <transition name="fade">
      <product-sidebar
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

    <product-tabs
      :product-tabs="productTabs"
      :selected-tab-index="selectedTabIndex"
      @selectTab="selectTab"
    />

    <product-reviews
        v-show="selectedTabIndex === 0"
        :product-reviews="productReviews"
    />

    <review-form
        v-show="selectedTabIndex === 1"
        :validation-errors="validationErrors"
        :product-reviews="productReviews"
        @addReview="addReview"
    />

  </div>
</template>

<script>
import ProductHero from "@/components/Product/ProductHero/ProductHero";
import ProductInfo from "@/components/Product/ProductInfo/ProductInfo";
import ProductFeatures from "@/components/Product/ProductFeatures/ProductFeatures";
import ProductHighlights from "@/components/Product/ProductHighlights/ProductHighlights";
import ProductReviews from "@/components/Product/ProductReviews/ProductReviews";
import ReviewForm from "@/components/Product/ReviewForm/ReviewForm";
import ProductSidebar from "@/components/Product/ProductSidebar/ProductSidebar";
import ProductTabs from "@/components/Product/ProductTabs/ProductTabs";

export default {
  name: 'SingleProductPage',
  components: {
    ProductTabs,
    ProductHero,
    ProductInfo,
    ProductFeatures,
    ProductHighlights,
    ProductReviews,
    ReviewForm,
    ProductSidebar,
  },
  props: {
  },
  data() {
    return {
      /* Product Hero */
      productName: 'Tesla Model X',
      productExcerpt: 'Highest performing SUV ever built',
      productHeroImg: '../../assets/img/perf-x.png',
      productHeroImgAlt: 'Tesla Model X',
      productHeroCta: 'ORDER NOW',
      productHeroCtaScope: '#info',
      hasBox: true,
      boxColor: '#97B8DB',

      /* Product Info */
      productUnderTag: 'Plaid',
      productDescription: 'Long Range and Plaid platforms unite powertrain and battery technologies for unrivaled performance, range and efficiency. New module and pack thermal architecture allows faster charging and gives you more power and endurance in all conditions.',
      productCtaHeading: 'Check more at Tesla website!',
      productCtaLink: 'https://www.tesla.com/modelx',

      /* Page Functionality */
      renderFeatures: false,

      /* Product Data */
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

      /* Reviews */
      productReviews: [],

      /* Validation */
      validationErrors: [],

      /* Tabs */
      productTabs: [
        {
          "tabIndex": 0,
          "tabContent": "Reviews"
        },
        {
          "tabIndex": 1,
          "tabContent": "Write a Review"
        },
      ],
      selectedTabIndex: 0,
    }
  },
  methods: {
    // Add Highlighted Feature to Cart
    // Close/Open Cart (Sidebar)
    toggleSidebar() {
      this.renderFeatures = !this.renderFeatures;
    },

    updateProduct(index) {
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
    },

    addReview(productReview) {
      this.productReviews.push(productReview);
    },

    selectTab(index) {
      this.selectedTabIndex = index;
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
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./SingleProductPage.scss" />
