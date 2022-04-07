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
            @click="gameClick(item)"
          ></GameButton>
        </div>
      </div>
      <div class="content__options">
        <div class="level">
          Choose level:
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
          Current round: {{ currentRound }}
          <div class="lose-note" v-if="lose">Вы проиграли. :с</div>
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
          background: "red",
        },
        {
          id: 2,
          background: "yellow",
        },
        {
          id: 3,
          background: "blue",
        },
        {
          id: 4,
          background: "green",
        },
      ],
      gameLevel: ["Easy", "Normal", "Hard"],
      currentLevel: "",
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
      this.gameChoice.forEach((i, index) => this.highlight(index * 1000, i));
      this.highlight(this.gameChoice.length * 1000, -1);
    },

    highlight(delay, id) {
      setTimeout(() => {
        this.activeButton = -1;
        setTimeout(() => (this.activeButton = id), 100);
      }, delay);
    },
  },

  computed: {
    currentRound() {
      return this.gameChoice.length;
    },
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
  }

  &__options {
    .level {
      display: flex;
      flex-direction: column;
    }
  }
}
</style>
