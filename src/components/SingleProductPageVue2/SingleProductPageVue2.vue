<template>
  <div class="product">
    <div class="product__column">
      <img class="product__image" src="../../assets/img/tesla-model-x-on-road.jpeg" alt="Picture of Tesla Model X" />
    </div>
    <div class="product__column">
        <h1 class="product__heading">{{ productName }}</h1>
        <p class="product__under-tag">{{ productUnderTag }}</p>
        <div class="product__column-description-box">
          <p class="product__description">{{ productDescription }}</p>
        </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SingleProductPageVue2',
  props: {
    productName: String,
    productUnderTag: String,
    productDescription: String,
  },
  data() {
    return {
      productName: 'Tesla Model X',
      productUnderTag: 'Plaid',
      productDescription: 'Long Range and Plaid platforms unite powertrain and battery technologies for unrivaled performance, range and efficiency. New module and pack thermal architecture allows faster charging and gives you more power and endurance in all conditions.',
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="src/components/SingleProductPageVue2/SingleProductPageVue2.scss" />
