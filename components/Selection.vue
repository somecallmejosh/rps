<template>
  <button :class="option" :disabled="state == 'disabled'">
    <rock v-if="option == 'rock'" />
    <paper v-if="option == 'paper'" />
    <scissors v-if="option == 'scissors'" />
  </button>
</template>

<script>
import Paper from "~/components/icons/Paper.vue";
import Rock from "~/components/icons/Rock.vue";
import Scissors from "~/components/icons/Scissors.vue";
export default {
  components: { Paper, Rock, Scissors },

  props: {
    state: {
      type: String
    },
    option: {
      type: String,
      validator: function(value) {
        return ["rock", "paper", "scissors"].indexOf(value) !== -1;
      }
    }
  }
};
</script>

<style scoped>
button {
  align-content: center;
  appearance: none;
  background: #fff;
  border-radius: 100%;
  border: 0;
  box-shadow: inset 0 5px 0 #ccc;
  cursor: pointer;
  display: inline-flex;
  height: 8rem;
  justify-content: center;
  position: relative;
  transition: background-color 0.2s;
  width: 8rem;
}

button:hover {
  background-color: #f4f4f4;
}

button svg {
  fill: #3b4262;
}

button::after,
button::before {
  border-radius: 100%;
  content: " ";
  display: block;
  height: 10rem;
  left: -1rem;
  position: absolute;
  top: -1rem;
  width: 10rem;
  z-index: -1;
}

button.paper::after {
  background-color: hsl(230, 89%, 65%);
  box-shadow: inset 0 -5px 0 hsl(230, 89%, 62%);
}

button.rock::after {
  background-color: hsl(349, 70%, 56%);
  box-shadow: inset 0 -5px 0 hsl(349, 71%, 52%);
}

button.scissors::after {
  background-color: hsl(40, 84%, 53%);
  box-shadow: inset 0 -5px 0 hsl(39, 89%, 49%);
}

button[disabled] {
  background-color: #e1e4ed;
  box-shadow: initial;
  pointer-events: none;
}

button[disabled]::after {
  background-color: #b9bacc;
  box-shadow: initial;
}

button[disabled] svg {
  fill: #8a8fac;
}

button.mySelection::before {
  box-shadow: 0 0 0 28px #2b3a59, 0 0 0 56px #263554, 0 0 0 80px #202f4e;
}
</style>