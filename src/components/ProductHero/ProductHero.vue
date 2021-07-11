<template>
  <div
      id="hero"
      class="hero"
  >
    <div class="hero__content">
      <img
          class="hero__img"
          :src="productHeroImg"
          :alt="productHeroImgAlt"
      />
    </div>
    <div
        class="hero__box-wrapper"
        v-if:="hasBox === true"
    >
      <div class="hero__box">
        <div class="hero__text-box">
          <h1 class="hero__heading">
            {{ productName }}
          </h1>
          <p class="hero__tag">
            {{ productExcerpt }}
          </p>
        </div>
        <a
            class="hero__box-cta"
            :href="productHeroCtaScope"
        >
          <p class="cta">
            {{ productHeroCta }}
          </p>
        </a>
      </div>
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
  data() {
    return {
       /* width: 1,
       height: 1,
       mousePosX: 0,
       mousePosY: 0, */

    }
  },
  mounted() {
     // document.addEventListener('mousemove', this.parallaxMove);
  },
  destroyed() {
     // document.removeEventListener('mousemove', this.parallaxMove)
  },
  methods: {

    /* Old Parallax Function */
     /*parallaxMove(event) {
       const element = document.querySelector(".hero__box:after");

       this.width = window.innerWidth/2;
       this.height = window.innerHeight/2;
       this.mousePosX = event.clientX;
       this.mousePosY = event.clientY;

       let firstLayer = `${30 - (this.mousePosX - this.width) * 0.05}% ${50 - (this.mousePosY - this.height) * 0.02}%`;
       let secondLayer = `${50 - (this.mousePosX - this.width) * 0.02}% ${50 - (this.mousePosY - this.height) * 0.02}%`;
       let thirdLayer = `${50 - (this.mousePosX - this.width) * 0.01}% ${140 - (this.mousePosY - this.height) * 0.01}%`;

       element.style.backgroundPosition = `${thirdLayer}, ${secondLayer}, ${firstLayer}`;
     },*/
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductHero.scss" />