<template>
  <div id="app">
<Tooltip content="this is a tip" placement="bottom" ><div class="btn">bottom tip message</div></Tooltip>
<Slider v-model="value"></Slider>
    <router-view/>
  </div>
</template>
<script>
import Tooltip from './components/tooltip.vue'
import Slider from './components/slider.vue'
export default{
  components: {
    Tooltip,
    Slider
  },
  data(){
    return{
      value:25
    }
  }
}
</script>
<style lang="less">
#app {
  padding: 50px;
  margin: 0;
  display: flex;
  justify-content: space-around;
  align-items: center;
  .btn{
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
    transform: translate3d(0,0,0);
    transition: color .2s linear,background-color .2s linear,border .2s linear;
    color: #657180;
    background-color: #f7f7f7;
    border-color: #d7dde4;
  }
}
</style>
