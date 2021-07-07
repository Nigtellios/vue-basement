<template>
  <single-product-page />
</template>

<script>
import SingleProductPage from './components/SingleProductPage/SingleProductPage.vue';
import ProductHero from './components/ProductHero/ProductHero.vue';
import ProductFeatures from './components/ProductFeatures/ProductFeatures.vue';
import ProductHighlights from './components/ProductHighlights/ProductHighlights.vue';
import Sidebar from "@/components/Sidebar/Sidebar.vue";

export default {
  name: 'App',
  components: {
    SingleProductPage,
    ProductHero,
    ProductFeatures,
    ProductHighlights,
    Sidebar,
  },
}
</script>
