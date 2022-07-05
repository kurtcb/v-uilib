<template>
  <div>
    <div class="slider">
      <div
        class="slider-bar-wrap"
        ref="sliderBarWrap"
        @click.self="sliderClick"
      >
        <div class="slider-bar" ref="sliderBar"></div>
      </div>
      <div class="button-wrap" @mousedown="mousedown($event)" ref="btn">
        <Tooltip :content="this.currentValue + ''" placement="top"
          ><div class="button"></div
        ></Tooltip>
      </div>
    </div>
  </div>
</template>

<script>
import Tooltip from "./tooltip.vue";
export default {
  components: {
    Tooltip,
  },
  props:{
      value: { type: Number, default: 0 },
  },
  data() {
    return {
      starX: null,
      currentX: null,
      drag: null,
      mouseupPos: 0,
      max: null,
      currentValue: 0,
    };
  },
  watch:{
     value(val){
      console.log(val);
    }
  },
  methods: {
    setClientX(e) {
      return e.clientX;
    },
    mousedown(e) {
      // 点击元素边缘快速拖拽可能会有mouseup没有触发的bug
      e.preventDefault();
      this.drag = true;
      this.starX = this.setClientX(e);
      // this.$nextTick(()=>{
      this.max = this.$refs.sliderBarWrap.offsetWidth;
      // })
      // 注册到全局以免纵向移除dom后滑动无效
      window.addEventListener("mousemove", this.mousemove);
      window.addEventListener("mouseup", this.mouseup);
    },
    mousemove(e) {
      const btnOffset = this.setClientX(e) - this.starX;
      if (
        this.drag &&
        +this.mouseupPos + btnOffset <= this.max &&
        +this.mouseupPos + btnOffset >= 0
      ) {
        this.$nextTick(() => {
          this.$refs.btn.style.left = +this.mouseupPos + btnOffset + "px";
          this.$refs.sliderBar.style.width =
            +this.mouseupPos + btnOffset + "px";
          this.currentValue = parseInt(
            ((+this.mouseupPos + btnOffset) / +this.max) * 100
          );
        });
      }
    },
    mouseup() {
      this.drag = false;
      // 页面渲染后触发防止$refs undefined
      this.$nextTick(() => {
        this.mouseupPos = this.$refs.btn.style.left.substr(
          0,
          this.$refs.btn.style.left.length - 2
        );
      });
    },
    sliderClick(e) {
      this.$nextTick(() => {
        this.max = this.$refs.sliderBarWrap.offsetWidth;
        this.$refs.btn.style.left = e.offsetX + "px";
        this.$refs.sliderBar.style.width = e.offsetX + "px";
        this.currentValue = parseInt((+e.offsetX / +this.max) * 100);
      });
    },
  },
};
</script>

<style lang="less" scoped>
.slider {
  width: 500px;
  height: 4px;
  position: relative;
  cursor: pointer;
  .slider-bar-wrap {
    position: relative;
    width: 100%;
    height: 100%;
    background-color: #ccc;
    .slider-bar {
      position: absolute;
      height: 100%;
      background-color: skyblue;
      // 鼠标事件失效并穿透该元素
      pointer-events: none;
    }
  }
  .button-wrap {
    height: 18px;
    width: 18px;
    position: absolute;
    top: -7px;
    .button {
      height: 12px;
      width: 12px;
      background-color: #fff;
      border: 3px solid skyblue;
      border-radius: 50%;
    }
  }
}
</style>