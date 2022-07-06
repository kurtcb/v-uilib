<template>
  <div class="pane" v-show="visibility"><slot></slot></div>
</template>

<script>
export default {
  inject: ["TabsInstance"],
  data() {
    return {
    };
  },
  computed: {
    visibility() {
      return this.TabsInstance.activeName == this.name ? true : false
    }
  },
  props: {
    label: {
      type: String,
    },
    name: {
      type: String,
    },
  },
  mounted() {
    this.TabsInstance.updateNavTab({name:this.name,label:this.label});
  },
};
</script>

<style>
</style>