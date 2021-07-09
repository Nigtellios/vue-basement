<template>
  <navigation />
  <single-product-page />
  <main-footer />
</template>

<script>
import SingleProductPage from './components/SingleProductPage/SingleProductPage.vue';
import ProductInfo from './components/ProductInfo/ProductInfo.vue';
import ProductFeatures from './components/ProductFeatures/ProductFeatures.vue';
import ProductHighlights from './components/ProductHighlights/ProductHighlights.vue';
import Sidebar from "@/components/Sidebar/Sidebar.vue";
import Navigation from "@/components/Navigation/Navigation";
import MainFooter from "@/components/MainFooter/MainFooter";

export default {
  name: 'App',
  components: {
    MainFooter,
    Navigation,
    SingleProductPage,
    ProductInfo,
    ProductFeatures,
    ProductHighlights,
    Sidebar,
  },
}
</script>
