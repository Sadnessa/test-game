<template>
  <button :style="{ 'background' : bgColor}">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    bgColor: {
      type: String,
      required: true,
    }
  }
}
</script>

<style lang="scss" scoped>
button {
  position: relative;
  border-radius: 6px;
  border: none;
  padding: 30px;
  margin: 4px;

  &:hover {
    &:after {
      content: "";
      position: absolute;
      width: 100%;
      height: 100%;
      top: 0px;
      left: 0px;
      background: rgba(0, 0, 0, 0.123);
      border-radius: inherit;
    }
  }
}
</style>
