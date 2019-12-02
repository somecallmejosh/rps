<template>
  <component :is="layout">
    <slot></slot>
  </component>
</template>

<script>
export default {
  props: {
    layout: {
      type: String,
      default: "div"
    },
    align: {
      type: String
    },
    justify: {
      type: String
    }
  }
};
</script>

<style scoped>
div {
  display: flex;
}
</style>