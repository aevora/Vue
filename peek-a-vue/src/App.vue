<template>
  <AppHeader />
  <NewGameButton :newPlayer="newPlayer" @start-new-game="startNewGame" />
  <GameBoard :cardList="cardList" :status="status" @flip-card="flipCard"/>
  <AppFooter />
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import { ref, watch } from "vue";
import { launchConfetti } from "./utilities/confetti";

import NewGameButton from "./components/NewGameButton.vue";
import GameBoard from "./components/GameBoard.vue";
import AppFooter from "./components/AppFooter.vue";
import createDeck from "./features/createDeck";
import createGame from "./features/createGame";
import halloweenDeck from "./data/halloweenDeck.json";

export default {
  name: "App",
  components: {
    AppHeader,
    NewGameButton,
    AppFooter,
    GameBoard,
  },
  setup() {
    const { cardList } = createDeck(halloweenDeck);
    const {
      newPlayer,
      startGame,
      restartGame,
      matchesFound,
      status,
    } = createGame(cardList);
    const userSelection = ref([]);

    const startNewGame = () => {
      if (newPlayer) {
        startGame();
      } else {
        restartGame();
      }
    };

    const flipCard = (payload) => {
      cardList.value[payload.position].visible = true;

      if (userSelection.value[0]) {
        if (
          userSelection.value[0].position === payload.position &&
          userSelection.value[0].faceValue === payload.faceValue
        ) {
          return;
        } else {
          userSelection.value[1] = payload;
        }
      } else {
        userSelection.value[0] = payload;
      }
    };

    watch(
      userSelection,
      (currentValue) => {
        if (currentValue.length === 2) {
          const cardOne = currentValue[0];
          const cardTwo = currentValue[1];

          if (cardOne.faceValue === cardTwo.faceValue) {
            cardList.value[cardOne.position].matched = true;
            cardList.value[cardTwo.position].matched = true;
          } else {
            setTimeout(() => {
              cardList.value[cardOne.position].visible = false;
              cardList.value[cardTwo.position].visible = false;
            }, 2000);
          }
          userSelection.value.length = 0;
        }
      },
      { deep: true }
    );

    watch(matchesFound, (currentValue) => {
      if (currentValue === 8) {
        launchConfetti();
      }
    });

    return {
      cardList,
      flipCard,
      userSelection,
      status,
      newPlayer,
      startNewGame,
    };
  },
};
</script>

<style >
html,
body {
  margin: 0;
  padding: 0;
}

h1 {
  margin-top: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-image: url("/images/page-bg.png");
  background-color: #00070c;
  height: 100vh;
  color: #fff;
  padding-top: 60px;
}

.game-board {
  display: grid;
  grid-template-columns: repeat(4, 120px);
  grid-template-rows: repeat(4, 120px);
  grid-column-gap: 24px;
  grid-row-gap: 24px;
  justify-content: center;
}

.sr-only {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0, 0, 0, 0);
  border: 0;
}

.status {
  font-family: "Titillium Web", sans-serif;
}

.shuffle-card-move {
  transition: transform 0.8s ease-in;
}
</style>
