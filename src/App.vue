<template>
  <single-product-page-vue2 />
</template>

<script>
import SingleProductPageVue2 from './components/SingleProductPageVue2/SingleProductPageVue2.vue';
import ProductHeroVue2 from './components/ProductHeroVue2/ProductHeroVue2.vue';
import ProductFeaturesVue2 from './components/ProductFeaturesVue2/ProductFeaturesVue2.vue';
import ProductHighlightsVue2 from './components/ProductHighlightsVue2/ProductHighlightsVue2.vue';
import SidebarVue2 from "@/components/SidebarVue2/SidebarVue2.vue";

export default {
  name: 'App',
  components: {
    SingleProductPageVue2,
    ProductHeroVue2,
    ProductFeaturesVue2,
    ProductHighlightsVue2,
    SidebarVue2,
  },
}
</script>
