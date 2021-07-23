<template>
  <section class="write-review section--padding">

    <div
        class="reviews__handlers"
        v-if="validationErrors.length"
    >
      <div
          class="reviews__handlers-box"
          v-for="error in validationErrors"
          :key="error.heading"
      >
        <h4 class="reviews__handlers-heading">
          {{ error.heading }}
        </h4>
        <p class="reviews__handlers-content">
          {{ error.content }}
        </p>
      </div>

    </div>
    <div class="write-review__box">
      <form
          class="write-review__form"
          @submit.prevent="onSubmit(productReviews)"
      >
        <p class="write-review__form-row">
          <label for="userName">Name:</label>
          <input
              id="userName"
              v-model="userName"
          >
        </p>
        <p class="write-review__form-row">
          <label for="userReview">Review:</label>
          <textarea
              id="userReview"
              v-model="userReview"
          ></textarea>
        </p>
        <p class="write-review__form-row">
          <label for="userRating">Rating:</label>
          <select
              id="userRating"
              v-model.number="userRating"
          >
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
    validationErrors: {
      type: Array,
      required: true,
    },
    productReviews: {
      type: Array,
      required: true,
    }
  },
  data() {
    return {
      userID: 0,
      userName: null,
      userReview: null,
      userRating: null,
    }
  },
  methods: {
    onSubmit(productReviews) {
      if (this.userName && this.userReview && this.userRating) {

        // Create Review Object
        let productReview = {
          id: this.userID,
          name: this.userName,
          review: this.userReview,
          rating: this.userRating
        }

        // Add +1 to UserID after first Submit
        this.userID === 0 ? this.userID++ : this.userID = null;

        // Check length of table with currently added Reviews
        for (let i = 0; i < productReviews.length; i++) {
          this.userID = productReviews.length + 1;
        }

        // Add Review and clear data with error table
        this.$emit('addReview', productReview);
        this.name = null;
        this.review = null;
        this.rating = null;
        this.validationErrors.splice(0, this.validationErrors.length);

      } else {

        // Display only current errors, empty an array if there is more than 1 object.
        for (let j = 0; j < this.validationErrors.length; j++) {
          if (this.validationErrors.length >= 1) {
            this.validationErrors.splice(0, this.validationErrors.length);
          }
        }

        // Push Error Messages after Checking length every time when ELSE occurs
        if (!this.userName) {
          this.validationErrors.push(
              {
                "heading": "Name required",
                "content": "Please enter your name!"
              }
          );
        } if (!this.userReview) {
          this.validationErrors.push(
              {
                "heading": "Content required",
                "content": "Please write something about this product!"
              }
          );
        } if (!this.userRating) {
          this.validationErrors.push(
              {
                "heading": "Rating required",
                "content": "Please rate this product from 1 to 5!"
              }
          );
        }
      }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ReviewForm.scss" />