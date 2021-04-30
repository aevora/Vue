<template>
  <button v-if="newPlayer" @click="startNewGame" :class="$style.button">
    <img src="/images/play.svg" alt="Restart Icon" />
    Start Game
  </button>
  <button v-else @click="startNewGame" :class="$style.button">
    <img src="/images/restart.svg" alt="Restart Icon" />
    Restart Game
  </button>
</template>
:
<script>
export default {
  props: {
    newPlayer: {
      type: Boolean,
      default: true,
    },
  },
  setup(props, context) {
    const startNewGame = () => context.emit("start-new-game");

    return {
      startNewGame,
    };
  },
};
</script>

<style module>
.button {
  background-color: #e78805;
  color: white;
  padding: 8px 16px 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto 30px;
  font-weight: bold;
  font-family: "Titillium Web", sans-serif;
  font-weight: bold;
  font-size: 1rem;
  border: 0;
  border-radius: 10px;
  transition: 0.2s all ease-in;
  border: 2px solid #e78805;
}

.button:hover {
  border: 2px solid #e78805;
  background-color: transparent;
}

.button img {
  padding-right: 12px;
  transition: 0.2s opacity ease-in;
}
</style>