<template>
  <div class="hero">
    <div class="hero__content">
      <div class="hero__text-box">
        <h1 class="hero__heading">
          {{ productName }}
        </h1>
        <p class="hero__tag">
          {{ productExcerpt }}
        </p>
      </div>
      <img
          class="hero__img"
          :src="productHeroImg"
          :alt="productHeroImgAlt"
      />
    </div>
    <div
        class="hero__box"
        v-if:="hasBox === true"
    >
      <a
          class="hero__box-cta"
          :href="productHeroCtaScope"
      >
        {{ productHeroCta }}
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductHero',
  props: {
    productName: {
      type: String,
      required: true,
    },
    productExcerpt: {
      type: String,
      required: true,
    },
    productHeroImg: {
      type: String,
      required: true,
    },
    productHeroImgAlt: {
      type: String,
      required: true,
    },
    productHeroCta: {
      type: String,
      required: true,
    },
    productHeroCtaScope: {
      type: String,
      required: true,
    },
    hasBox: {
      type: Boolean,
      required: true,
    },
    boxColor: {
      type: String,
      required: true,
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductHero.scss" />