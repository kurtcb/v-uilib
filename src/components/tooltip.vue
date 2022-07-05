<template>
  <div class="tooltip">
    <div
      class="tooltip-rel"
      ref="reference"
      @mouseenter="handleShowPopper"
      @mouseleave="handleClosePopper"
    >
      <slot></slot>
    </div>
    <div
      class="tooltip-popper"
      ref="popper"
      v-show="visible"
      :placement="placement"
    >
      <div class="tooltip-content">
        <div class="tooltip-arrow"></div>
        <div class="tooltip-inner">
          <slot name="content">{{ content }}</slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      visible: false,
    };
  },
  props: {
    content: { type: String, default: "" },
    placement: {
      default: "bottom",
    },
  },
  methods: {
    handleShowPopper() {
      this.visible = true;
    },
    handleClosePopper() {
      this.visible = false;
    },
  },
};
</script>

<style lang="less" scoped>
.tooltip {
  display: inline-block;
  position: relative;
  &-rel {
    display: inline-block;
    position: relative;
    width: inherit;
  }
  &-popper {
    position: absolute;
    transform-origin: center top;
    padding: 8px 0 5px 0;
    visibility: visible;
    font-size: 12px;
    line-height: 1.5;
    display: block;
    visibility: visible;
    font-size: 12px;
    line-height: 1.5;
    z-index: 1060;
    &[placement^="bottom"] .tooltip-arrow {
      top: 3px;
      left: 50%;
      margin-left: -5px;
      border-width: 0 5px 5px;
      border-bottom-color: rgba(70, 76, 91, 0.9);
    }
    &[placement^="bottom"] {
      left: 50%;
      transform: translateX(-50%);
    }
    &[placement^="top"] .tooltip-arrow {
      bottom: 0px;
      left: 50%;
      margin-left: -5px;
      border-width: 5px 5px 0;
      border-top-color: rgba(70, 76, 91, 0.9);
    }
    &[placement="top"] {
      left: 50%;
      top: 0;
      transform: translateX(-50%) translateY(-100%);
    }
    &[placement^="left"] .tooltip-arrow {
      top: 50%;
      margin-top: -5px;
      right: -5px;
      border-width: 5px 0 5px 5px;
      border-left-color: rgba(70, 76, 91, 0.9);
    }
    &[placement="left"] {
      left: 0;
      top: 50%;
      transform: translateY(-50%) translateX(-100%);
      margin-left: -8px;
    }

    &[placement^="right"] .tooltip-arrow {
      top: 50%;
      left: -5px;
      border-width: 5px 5px 5px 0;
      border-right-color: rgba(70, 76, 91, 0.9);
      transform: translateY(-50%);
    }
    &[placement="right"] {
      left: 100%;
      top: 50%;
      transform: translateY(-50%);
      margin-left: 8px;
    }
  }
  &-inner {
    max-width: 250px;
    padding: 8px 12px;
    color: #fff;
    text-align: left;
    text-decoration: none;
    background-color: rgba(70, 76, 91, 0.9);
    border-radius: 4px;
    box-shadow: 0 1px 6px rgb(0 0 0 / 20%);
    white-space: nowrap;
  }
  &-arrow {
    position: absolute;
    width: 0;
    height: 0;
    border-color: transparent;
    border-style: solid;
  }
}
</style>