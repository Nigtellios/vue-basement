<template>
  <single-product-page />
</template>

<script>
import SingleProductPage from './components/SingleProductPage/SingleProductPage.vue';
import ProductInfo from './components/ProductInfo/ProductInfo.vue';
import ProductFeatures from './components/ProductFeatures/ProductFeatures.vue';
import ProductHighlights from './components/ProductHighlights/ProductHighlights.vue';
import Sidebar from "@/components/Sidebar/Sidebar.vue";

export default {
  name: 'App',
  components: {
    SingleProductPage,
    ProductInfo,
    ProductFeatures,
    ProductHighlights,
    Sidebar,
  },
}
</script>
