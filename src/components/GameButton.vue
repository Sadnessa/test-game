<template>
  <button
    :style="{ background: bgColor }"
    :class="{ 'btn--active': isActive }"
    @click="onClick"
  >
    <slot></slot>
    <audio ref="audio" :src="compAudio"></audio>
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

    id: {
      type: Number,
      required: true,
    },
  },

  watch: {
    isActive(newValue) {
      if (newValue) {
        this.playSound()
      }
    },
  },

  computed: {
    compAudio() {
      if (this.id == 2) {
        return require("../audio/sounds_2.mp3");
      }
      if (this.id == 3) {
        return require("../audio/sounds_3.mp3");
      }
      if (this.id == 4) {
        return require("../audio/sounds_4.mp3");
      }
      return require("../audio/sounds_1.mp3");
    },
  },

  methods: {
    onClick() {
      this.$emit("click");
      this.playSound();
    },

    playSound() {
      this.$refs.audio.play();
    }
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
    background: rgba(255, 255, 255, 0.322);
    border-radius: inherit;
    outline: 2px solid rgb(201, 201, 201);
    transition: all ease-in-out 0.2s;
  }

  &:hover {
    &:after {
      background: rgba(0, 0, 0, 0.2);
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
        outline: 2px solid rgba(0, 0, 0, 0.849);
      }
    }
  }
}
</style>
