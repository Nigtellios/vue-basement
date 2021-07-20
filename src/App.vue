<template>
  <main-navigation
      :nav-items="navItems"
      :shop-nav="shopNav"
  />

    <single-product-page />

  <main-footer />
</template>

<script>
import SingleProductPage from '@/components/SingleProductPage/SingleProductPage.vue';
import ProductInfo from '@/components/ProductInfo/ProductInfo.vue';
import ProductFeatures from '@/components/ProductFeatures/ProductFeatures.vue';
import ProductHighlights from '@/components/ProductHighlights/ProductHighlights.vue';
import ProductReviews from "@/components/ProductReviews/ProductReviews";
import ReviewForm from "@/components/ReviewForm/ReviewForm";
import ProductSidebar from "@/components/ProductSidebar/ProductSidebar.vue";
import MainNavigation from "@/components/MainNavigation/MainNavigation.vue";
import MainFooter from "@/components/MainFooter/MainFooter.vue";

export default {
  name: 'App',
  components: {
    MainFooter,
    MainNavigation,
    SingleProductPage,
    ProductInfo,
    ProductFeatures,
    ProductHighlights,
    ProductReviews,
    ReviewForm,
    ProductSidebar,
  },
  data() {
    return {
      websiteLogo: '../../assets/img/perf-x.png',
      navItems: [
        {
          "itemID": 0,
          "itemName": "Model X",
          "itemRoute": "#hero",
        },
        {
          "itemID": 1,
          "itemName": "Features",
          "itemRoute": "#features",
        },
        {
          "itemID": 2,
          "itemName": "Customize",
          "itemRoute": "#customize",
        },
        {
          "itemID": 3,
          "itemName": "Order",
          "itemRoute": "#order",
        },
      ],
      shopNav: [
        {
          "itemID": 0,
          "itemIcon": "../../assets/icons/account.svg",
          "itemRoute": "#account",
        },
        {
          "itemID": 1,
          "itemIcon": "../../assets/icons/order.svg",
          "itemRoute": "#order",
        },
        {
          "itemID": 2,
          "itemIcon": "../../assets/icons/cart.svg",
          "itemRoute": "#sidebar",
        },
      ],
    }
  },
  methods: {

  },
}
</script>
