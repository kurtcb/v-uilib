<template>
  <div id="app">
    <Tooltip content="this is a tip" placement="bottom"
      ><div class="btn">bottom tip message</div></Tooltip
    >
    <Slider v-model="value"></Slider>
    <Slider v-model="value"></Slider>
    <button @click="showModel = true">show model</button>
    <Model :showModel.sync="showModel" title="提示">
      <p v-for="item in data" :key="item.index">{{ item.name }}</p>
      <span slot="foot"
        ><button class="btn" @click="cancel">取消</button
        ><button
          class="btn"
          style="background-color: #409eff; color: #fff; margin-left: 20px"
          @click="confirm"
        >
          确定
        </button></span
      >
    </Model>
    <Tabs value="name1">
      <Tabs-pane label="tab1" name="name1">content1</Tabs-pane>
      <Tabs-pane label="tab2" name="name2">content2</Tabs-pane>
    </Tabs>
    <router-view />
  </div>
</template>
<script>
import Tooltip from "./components/tooltip.vue";
import Slider from "./components/slider.vue";
import Model from "./components/model.vue";
import Tabs from "./components/tabs/tabs.vue";
import TabsPane from "./components/tabs/pane.vue";
export default {
  components: {
    Tooltip,
    Slider,
    Model,
    Tabs,
    TabsPane
  },
  data() {
    return {
      value: 25,
      showModel: false,
      data:[]
    };
  },
  mounted() {
    setTimeout(() => {
      this.data = [
        { name: "oooooooooooooooooooo", index: 0 },
        { name: "oooooooooooooooooooo", index: 1 },
        { name: "oooooooooooooooooooo", index: 2 },
        { name: "oooooooooooooooooooo", index: 3 },
      ];
    }, 3000);
  },
  methods: {
    // close(e) {
    //   this.showModel = e;
    // },
    confirm() {
      console.log("comfirm!");
      this.showModel = false;
    },
    cancel() {
      console.log("cancel!");
      this.showModel = false;
    },
  },
};
</script>
<style lang="less">
#app {
  padding: 50px;
  margin: 0;
  display: flex;
  justify-content: space-around;
  align-items: center;
  .btn {
    display: inline-block;
    margin-bottom: 0;
    font-weight: 400;
    text-align: center;
    vertical-align: middle;
    -ms-touch-action: manipulation;
    touch-action: manipulation;
    cursor: pointer;
    background-image: none;
    border: 1px solid transparent;
    white-space: nowrap;
    line-height: 1.5;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
    padding: 6px 15px;
    font-size: 12px;
    border-radius: 4px;
    transform: translate3d(0, 0, 0);
    transition: color 0.2s linear, background-color 0.2s linear,
      border 0.2s linear;
    color: #657180;
    background-color: #f7f7f7;
    border-color: #d7dde4;
  }
}
</style>
