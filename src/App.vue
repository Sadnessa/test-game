<template>
  <div class="content">
    <div class="content__title">Simon the game</div>
    <div class="content__main">
      <div class="content__game">
        <div class="items">
          <GameButton
            v-for="item in buttons"
            :key="item.id"
            :bgColor="item.background"
            :isActive="item.id == activeButton"
            :id="item.id"
            @click="gameClick(item)"
          ></GameButton>
        </div>
      </div>
      <div class="content__options">
        <div class="level">
          <strong>Choose level:</strong>
          <label v-for="lvl in gameLevel" :key="lvl">
            <input
              type="radio"
              name="level"
              :value="lvl"
              v-model="currentLevel"
            />
            {{ lvl }}
          </label>
        </div>
        <button class="start" @click="startGame">Start game</button>
        <div class="current-state" v-if="currentRound">
          <strong>Current round:</strong> {{ currentRound }}
          <div class="lose-note" v-if="lose">
            Sorry! You lost! Your record is {{ currentRound }}.
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import GameButton from "./components/GameButton.vue";
import { randomNum } from "./utils/index";
export default {
  components: {
    GameButton,
  },

  data() {
    return {
      buttons: [
        {
          id: 1,
          background: "#ea5826",
        },
        {
          id: 2,
          background: "#febe5c",
        },
        {
          id: 3,
          background: "#3246a7",
        },
        {
          id: 4,
          background: "#00946d",
        },
      ],
      gameLevel: ["Easy", "Normal", "Hard"],
      currentLevel: "Easy",
      gameChoice: [],
      userChoice: [],
      activeButton: -1,
      lose: false,
    };
  },

  methods: {
    startGame() {
      this.userChoice = [];
      this.gameChoice = [];
      this.lose = false;
      this.newRound();
    },

    gameClick(item) {
      let lastIndex = this.userChoice.push(item.id) - 1;
      if (this.gameChoice[lastIndex] !== this.userChoice[lastIndex]) {
        this.lose = true;
        return;
      }
      if (this.gameChoice.length == this.userChoice.length) {
        return this.newRound();
      }
    },

    newRound() {
      this.userChoice = [];
      this.gameChoice.push(randomNum(1, 4));
      this.gameChoice.forEach((i, index) =>
        this.highlight(index * this.levelDelay, i)
      );
      this.highlight(this.gameChoice.length * this.levelDelay, -1);
    },

    highlight(delay, id) {
      setTimeout(() => {
        this.activeButton = -1;
        setTimeout(() => (this.activeButton = id), 1000);
      }, delay);
    },
  },

  computed: {
    currentRound() {
      return this.gameChoice.length;
    },

    levelDelay() {
      if (this.currentLevel == "Normal") {
        return 1000;
      }
      if (this.currentLevel == "Hard") {
        return 400;
      }
      return 1500;
    },
  },
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@300;500;&display=swap");

body {
  font-family: "Roboto", sans-serif;
  background-image: linear-gradient(
    92.7deg,
    rgba(245, 212, 212, 1) 8.5%,
    rgba(252, 251, 224, 1) 90.2%
  );
  margin: 0px;
  color: #101320ea;
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
  padding: 0px 10px;
  box-sizing: border-box;

  &__title {
    margin: 40px;
    font-size: 24px;
  }

  &__main {
    width: 100%;
    display: flex;
    justify-content: center;
  }

  &__game {
    display: flex;
    justify-content: center;
    margin-right: 20px;

    .items {
      width: 100%;
      height: 100%;
      max-width: 300px;
      max-height: 400px;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      margin: -6px;

      button {
        margin: 6px;
      }
    }
  }

  &__options {
    min-width: 260px;
    .start {
      position: relative;
      border: none;
      border-radius: 4px;
      padding: 12px;
      margin: 10px 0px;
      background: #c7a496;
      color: white;
      font-size: 18px;

      &:after {
        position: absolute;
        content: "";
        width: 100%;
        height: 100%;
        top: 0px;
        left: 0px;
        border-radius: inherit;
        background: transparent;
        transition: all ease-in-out 0.2s;
      }

      &:hover {
        &:after {
          background: rgba(255, 255, 255, 0.247);
        }
      }
    }

    .level {
      display: flex;
      flex-direction: column;
    }

    .current-state {
      margin: 10px 0px;
      .lose-note {
        margin: 16px 0px;
      }
    }
  }
}

@media screen and (max-width: 600px) {
  .content {
    &__main {
      flex-direction: column;
    }

    &__game {
      margin-right: 0px;
    }

    &__options {
      display: flex;
      flex-direction: column;
      align-items: center;
      margin-top: 30px;
    }
  }
}
</style>
