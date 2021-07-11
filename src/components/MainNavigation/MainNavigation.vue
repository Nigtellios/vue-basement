<template>
  <nav class="navigation">
    <div class="navigation__logo">
      <svg class="logotype" viewBox="0 0 342 35" xmlns="http://www.w3.org/2000/svg">
        <path
            d="M0 .1a9.7 9.7 0 007 7h11l.5.1v27.6h6.8V7.3L26 7h11a9.8 9.8 0 007-7H0zm238.6 0h-6.8v34.8H263a9.7 9.7 0 006-6.8h-30.3V0zm-52.3 6.8c3.6-1 6.6-3.8 7.4-6.9l-38.1.1v20.6h31.1v7.2h-24.4a13.6 13.6 0 00-8.7 7h39.9v-21h-31.2v-7h24zm116.2 28h6.7v-14h24.6v14h6.7v-21h-38zM85.3 7h26a9.6 9.6 0 007.1-7H78.3a9.6 9.6 0 007 7zm0 13.8h26a9.6 9.6 0 007.1-7H78.3a9.6 9.6 0 007 7zm0 14.1h26a9.6 9.6 0 007.1-7H78.3a9.6 9.6 0 007 7zM308.5 7h26a9.6 9.6 0 007-7h-40a9.6 9.6 0 007 7z"
            fill="">
        </path>
      </svg>
    </div>
    <div
        class="navigation__wrapper"
        v-if="navItems.length > 0"
    >
      <ul class="navigation__list">
        <li
            class="navigation__item"
            v-for="item in navItems"
            :key="item.itemID"
        >
          <a
              class="navigation__link"
              :href="item.itemRoute"
          >
            <p class="navigation__link-p">
              {{ item.itemName }}
            </p>
          </a>
        </li>
      </ul>
    </div>
    <div
        class="navigation__shop"
        v-if="shopNav.length > 0"
    >
      <ul class="navigation__shop-list">
        <li
            class="navigation__shop-list-item"
            v-for="item in shopNav"
            :key="item.itemID"
        >
          <a
              class="navigation__shop-list-item-link"
              :href="item.itemRoute"
          >
            <div class="navigation__shop-list-item-icon">
              <img
                :src="item.itemIcon"
              />
            </div>
          </a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script>
export default {
  name: 'Navigation',
  props: {
    navItems: {
      type: Array,
      required: true,
    },
    shopNav: {
      type: Array,
      required: true,
    }
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
<style lang="scss" src="./MainNavigation.scss" />