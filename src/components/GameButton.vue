<template>
  <button :style="{ background: bgColor }" :class="{ 'btn--active': isActive }" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<script>
export default {
  props: {
    bgColor: {
      type: String,
      required: true,
    },

    isActive: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style lang="scss" scoped>
button {
  position: relative;
  border-radius: 6px;
  border: none;
  padding: 60px;
  cursor: pointer;

  &:after {
    content: "";
    position: absolute;
    width: 100%;
    height: 100%;
    top: 0px;
    left: 0px;
    background: rgba(255, 255, 255, 0.5);
    border-radius: inherit;
  }
  
  &:hover {
    &:after {
      background: rgba(0, 0, 0, 0.1);
    }
  }

  &:active {
    &:after {
      background: transparent;
    }
  }

  &.btn {
    &--active {
      &:after {
        background: transparent;
        outline: 2px solid rgba(255, 255, 255, 0.849)
      }
    }
  }
}
</style>
