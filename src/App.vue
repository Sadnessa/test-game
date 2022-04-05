<template>
  <div class="content">
    <div class="content__title">Simon the game</div>
    <div class="content__game">
      <GameButton bgColor="red">dsdas</GameButton>
      <GameButton bgColor="yellow">dsdas</GameButton>
      <GameButton bgColor="green">dsdas</GameButton>
      <GameButton bgColor="blue">dsdas</GameButton>
    </div>
    <div class="content__btns">
      <button class="start">Start game</button>
    </div>
  </div>
</template>

<script>
import GameButton from "./components/GameButton.vue";

export default {
  components: {
    GameButton,
  },
};
</script>

<style lang="scss">
body {
  background: gray;
  margin: 0px;
}
</style>

<style lang="scss" scoped>
.content {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  width: 100%;
  height: 100vh;
}
</style>
