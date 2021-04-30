<script>
import Card from "../components/Card";

export default {
  components: {
    Card,
  },
  emits: {
    "flip-card": (payload) => (payload != null ? true : false),
  },
  props: {
    cardList: {
      type: Array,
      required: true,
    },
    status: {
      type: String,
      required: true,
    },
  },
  setup(props, context) {
    const selectCard = (payload) => {
      context.emit("flip-card", payload);
    };
    return {
      selectCard,
    };
  },
};
</script>

<template>
  <transition-group tag="section" class="game-board" name="shuffle-card">
    <Card
      v-for="card in cardList"
      :key="`${card.value}-${card.variant}`"
      :matched="card.matched"
      :value="card.value"
      :visible="card.visible"
      :position="card.position"
      @select-card="selectCard"
    />
  </transition-group>
  <h2 class="status">{{ status }}</h2>
</template>
