<template>
  <section class="write-review">
    <div class="write-review__box">
      <form
          class="write-review__form"
          @submit.prevent="onSubmit"
      >
        <p class="write-review__form-row">
          <label for="userName">Name:</label>
          <input id="userName" v-model="userName">
        </p>
        <p class="write-review__form-row">
          <label for="userReview">Review:</label>
          <textarea id="userReview" v-model="userReview"></textarea>
        </p>
        <p class="write-review__form-row">
          <label for="userRating">Rating:</label>
          <select id="userRating" v-model.number="userRating">
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
          </select>
        </p>
        <p class="write-review__form-row">
          <input type="submit" value="Submit">
        </p>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ReviewForm',
  props: {

  },
  data() {
    return {
      userName: null,
      userReview: null,
      userRating: null,
    }
  },
  methods: {
    onSubmit() {
      let productReview = {
        name: this.userName,
        review: this.userReview,
        rating: this.userRating,
      }
      this.$emit('review-submitted', productReview);
      this.name = null;
      this.review = null;
      this.rating = null;
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ReviewForm.scss" />