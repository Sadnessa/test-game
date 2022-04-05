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
