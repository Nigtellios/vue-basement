<template>
  <section class="reviews section--padding">
    <div class="reviews__box">
      <div
          class="single-item"
          v-for="review in productReviews"
          :key="review.name"
      >
        <div class="single-item__profile-picture">
          <img src="" alt="" />
        </div>
        <div class="single-item__content">
          <h4 class="single-item__content-heading">
            {{ review.name }}
          </h4>
          <div class="single-item__content-rating">
            {{ review.rating }}
          </div>
          <p class="single-item__content-paragraph">
            {{ review.review }}
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductReviews',
  props: {
    productReviews: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {

    }
  },
  methods: {

  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductReviews.scss" />