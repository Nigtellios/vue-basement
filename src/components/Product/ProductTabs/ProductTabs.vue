<template>
  <section class="tabs section--padding">
    <div
        class="tabs__tab"
        :class="{ 'tabs__tab--active': selectedTabIndex === productTab.tabIndex }"
        v-for="productTab in productTabs"
        :key="productTab.tabIndex"
        @click="selectTab(productTab.tabIndex)"
    >
      <h4 class="tabs__tab-heading">
        {{ productTab.tabContent }}
      </h4>
    </div>
  </section>
</template>

<script>
export default {
  name: 'ProductTabs',
  props: {
    productTabs: {
      type: Array,
      required: true,
    },
    selectedTabIndex: {
      required: true,
    },
  },
  methods: {
    selectTab(index) {
      this.$emit('selectTab', index);
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" src="./ProductTabs.scss" />