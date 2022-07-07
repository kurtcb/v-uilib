<template>
  <div class="tabs">
    <div class="tab-nav" style="display: flex">
      <div
        class="tab-item"
        v-for="item in navList"
        :key="item.index"
        :class="{ 'tab-item-active': item.name == activeName }"
        @click="handelNavTab(item)"
        ref="tabItem"
      >
        {{ item.label }}
      </div>
      <div class="tab-bar" ref="tabBar"></div>
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
  mounted() {
    this.$nextTick(() => {
      this.$refs.tabBar.style.width =
        this.$refs.tabItem[this.getTabIndex(this.activeName)].clientWidth +
        "px";
    });
  },
  methods: {
    updateNavTab(nav) {
      this.navList.push(nav);
    },
    handelNavTab(item) {
      this.activeName = item.name;
      this.index = item.index;
      const index = this.getTabIndex(this.activeName);
      //   to do  如何实现bar宽度等于content不包含padding的宽度
      this.$nextTick(() => {
        const barWidth =
          this.$refs.tabItem[this.getTabIndex(this.activeName)].clientWidth +
          "px";
        this.$refs.tabBar.style.width = barWidth;
        let barOffset = 0;
        for (let i = 0; i < index; i++) {
          barOffset += this.$refs.tabItem[i].clientWidth;
        }
        this.$refs.tabBar.style.transform = `translate3d(${barOffset}px , 0px, 0px)`;
      });
    },
    getTabIndex(activeName) {
      return this.navList.findIndex((e) => e.name == activeName);
    },
  },
};
</script>

<style lang="less" scoped>
.tabs {
  .tab-nav {
    position: relative;
    .tab-item {
      padding: 0 20px;
      height: 40px;
      box-sizing: border-box;
      line-height: 40px;
      display: inline-block;
      font-size: 14px;
      font-weight: 500;
      color: #303133;
      cursor: pointer;
    }
    .tab-item:hover,
    .tab-item-active {
      color: #409eff;
    }
    .tab-bar {
      position: absolute;
      left: 0;
      bottom: 0;
      height: 2px;
      background-color: #409eff;
    }
  }
}
</style>