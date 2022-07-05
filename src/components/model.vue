<template>
  <div v-if="showModel">
    <div class="model-wrap" @click.self="close">
      <div class="model">
        <div class="model-content">
          <div class="model-head"><span>{{title}}</span> <i @click.self="close">X</i></div>
          <div class="model-body"><slot></slot></div>
          <div class="model-foot"> <slot name="foot"></slot></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    showModel: {
      type: Boolean,
    },
    title: {
      type: String,
    },
  },
  methods: {
    close() {
    //  $emit.sync update:  props的双向绑定
     this.$emit('update:showModel', false);
    },
  },
};
</script>

<style lang="less" scoped>
.model-wrap {
  position: fixed;
  left: 0;
  bottom: 0;
  top: 0;
  right: 0;
  background-color: rgba(55, 55, 55, 0.6);
  z-index: 999;
  display: flex;
  justify-content: center;
  .model {
    display: inline-block;
    width: 520px;
    height: 300px;
    background-color: #fff;
    position: relative;
    top: 200px;
    &-head {
      display: flex;
      justify-content: space-between;
      padding:20px 15px 0 15px;
    }
    &-body {
      padding: 20px 15px 0 15px;
    }
    &-foot {
      padding: 20px;
      display: flex;
      justify-content: end;
    }
  }
}
</style>