<template>
  <div class="content">
    <div class="content__title">Simon the game</div>
    <div class="content__main">
      <div class="content__game">
        <div class="row">
          <GameButton bgColor="red">dsdas</GameButton>
          <GameButton bgColor="yellow">dsdas</GameButton>
        </div>
        <div class="row">
          <GameButton bgColor="green">dsdas</GameButton>
          <GameButton bgColor="blue">dsdas</GameButton>
        </div>
      </div>
      <div class="content__options">
        <div class="level">
          Choose level:
          <label>
            <input type="radio" name="level" value="easy" />
            Easy
          </label>
          <label>
            <input type="radio" name="level" value="normal" />
            Normal
          </label>
          <label>
            <input type="radio" name="level" value="hard" />
            Hard
          </label>
        </div>
        <button class="start">Start game</button>
        <div class="current-state">
          Current round: __
          <div class="lose-note"></div>
        </div>
      </div>
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
  background: rgb(197, 197, 197);
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

  &__title {
    margin: 28px;
    font-size: 24px;
  }

  &__main {
    display: flex;
  }

  &__game {
    margin-right: 20px;

    .row {
      button {
        &:first-child {
          margin-right: 8px;
        }
      }

      &:first-child {
        margin-bottom: 8px;
      }
    }
  }

  &__options {
    .level {
     display: flex;
     flex-direction: column;
    }
  }
}
</style>
