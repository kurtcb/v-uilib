<template>
  <div class="tabs">
    <div class="tab-nav" style="display: flex">
      <div
        v-for="item in navList"
        :key="item.index"
        @click="handelNavTab(item)"
      >
        {{ item.label }}
      </div>
    </div>
    <div class="tab-content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
    },
  },
  data() {
    return {
      navList: [],
      activeName: this.value,
    };
  },
  provide() {
    return { TabsInstance: this };
  },
  mounted() {},
  methods: {
    updateNavTab(nav) {
      this.navList.push(nav);
    },
    handelNavTab(item) {
      this.activeName = item.name;
    },
  },
};
</script>

<style>
</style>