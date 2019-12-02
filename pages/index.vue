<template>
  <section class="wrapper">
    <header>
      <h1>Rock Paper Scissors</h1>
      <div class="score-board">
        <div>
          <h2>Score</h2>
          <span class="score">{{score}}</span>
        </div>
      </div>
    </header>
    <div v-if="gameOpen">
      <selection option="rock" @click.native="selection('rock')" />
      <selection option="paper" @click.native="selection('paper')" />
      <selection option="scissors" @click.native="selection('scissors')" />
    </div>
    <div v-if="!gameOpen">
      <div class="results-grid">
        <div>
          <selection :option="mySelection" class="mySelection" />
          <p>You picked</p>
        </div>

        <div>
          <selection :option="computerSelection" />
          <p>The house picked</p>
        </div>
      </div>

      <div class="results">
        <div>{{compareSelectionResults}}</div>
        <button @click="toggleGameState()">Play Again</button>
      </div>
    </div>
  </section>
</template>

<script>
import Selection from "~/components/Selection.vue";
export default {
  components: { Selection },
  data() {
    return {
      compareSelectionResults: "",
      mySelection: null,
      computerSelection: null,
      gameOpen: true,
      score: 0,
      options: [
        { value: "rock", beats: "scissors" },
        { value: "paper", beats: "rock" },
        { value: "scissors", beats: "paper" }
      ]
    };
  },
  methods: {
    compareSelections() {
      if (this.mySelection == this.computerSelection) {
        this.compareSelectionResults = "you tied";
        return;
      }
      this.options.forEach(option => {
        if (
          this.mySelection == option.value &&
          this.computerSelection == option.beats
        ) {
          this.compareSelectionResults = "you win";
        }

        if (
          this.mySelection == option.value &&
          this.computerSelection != option.beats
        ) {
          this.compareSelectionResults = "you lose";
        }
      });

      if (this.compareSelectionResults == "you win") {
        this.score += 1;
      }

      if (this.compareSelectionResults == "you lose") {
        this.score -= 1;
      }
    },
    selection(value) {
      this.mySelection = value;
      this.computerSelection = this.options[
        Math.floor(Math.random() * 3)
      ].value;
      this.toggleGameState(this.gameOpen);
    },
    toggleGameState(gameOpen) {
      if (!gameOpen) {
        this.mySelection = null;
        this.computerSelection = null;
      }
      this.compareSelectionResults = null;
      this.gameOpen = !this.gameOpen;
      this.compareSelections();
    }
  }
};
</script>

<style>
* {
  text-transform: uppercase;
}
button {
  margin: 2rem;
}

header {
  border: var(--header-outline) 0.2rem solid;
  border-radius: var(--border-radius);
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 1rem 1rem 1rem 2.3rem;
}
h1 {
  max-width: 5rem;
  line-height: 0.8;
}

.results {
  text-align: center;
}

.results-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  text-align: center;
}
.score-board {
  border-radius: var(--border-radius);
  background-color: #fff;
  margin-left: auto;
  text-align: center;
  color: black;
  display: flex;
  align-items: center;
  padding: 0 2rem;
}
</style>
