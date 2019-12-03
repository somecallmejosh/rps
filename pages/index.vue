<template>
  <section>
    <header>
      <h1>
        Rock
        <br />Paper
        <br />Scissors
      </h1>
      <div class="score-board">
        <div>
          <h2>Score</h2>
          <span class="score">{{score}}</span>
        </div>
      </div>
    </header>
    <main>
      <div v-if="gameOpen" class="game-pick">
        <div class="rock-wrapper">
          <selection option="rock" @click.native="selection('rock')" />
        </div>
        <div class="paper-wrapper">
          <selection option="paper" @click.native="selection('paper')" />
        </div>
        <div class="scissors-wrapper">
          <selection option="scissors" @click.native="selection('scissors')" />
        </div>
      </div>
      <div v-if="!gameOpen">
        <div class="results-grid">
          <div class="results-pick">
            <selection
              :option="mySelection"
              :class="{winner : compareSelectionResults == 'you win'}"
            />
            <p>You picked</p>
          </div>
          <div class="results">
            <p>{{compareSelectionResults}}</p>
            <button @click="toggleGameState()">Play Again</button>
          </div>
          <div class="results-pick">
            <selection
              :option="computerSelection"
              :class="{winner : compareSelectionResults == 'you lose'}"
            />
            <p>The house picked</p>
          </div>
        </div>
      </div>
    </main>
    <button class="rules-trigger">Rules</button>
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

section {
  padding: 30px 0;
}

h1,
h3,
p {
  text-shadow: 0 0 2px black;
}

main,
header {
  margin: 0 auto;
  width: calc(100% - 30px);
  max-width: 705px;
}

main {
  height: calc(85vh - 60px);
  display: flex;
  align-items: center;
  justify-content: center;
}

header {
  align-items: center;
  border: var(--header-outline) 0.2rem solid;
  border-radius: var(--border-radius);
  display: grid;
  grid-template-columns: 1fr 1fr;
  height: 15vh;
  padding: 0.5rem 0.5rem 0.5rem 1rem;
}

h1 {
  line-height: 0.8;
}

.game-pick {
  background: url(/images/bg-triangle.svg) top center no-repeat;
  background-size: contain;
  position: relative;
  height: 200px;
  width: 200px;
}

.game-pick > div {
  position: absolute;
}

.game-pick .rock-wrapper {
  left: 0;
  top: 0;
  transform: translateX(-50%) translateY(-50%);
}

.game-pick .paper-wrapper {
  right: 0;
  top: 0;
  transform: translateX(50%) translateY(-50%);
}

.game-pick .scissors-wrapper {
  left: 50%;
  bottom: 0;
  transform: translateX(-50%) translateY(25%);
}

.results-grid {
  display: grid;
  grid-template-columns: 1fr 2fr 1fr;
  text-align: center;
}

.results {
  text-align: center;
  margin-top: 200px;
}

.results p {
  font-size: 3rem;
  font-weight: bold;
  letter-spacing: 1px;
}

.results button {
  background-color: #fff;
  border: 0;
  border-radius: var(--border-radius);
  display: flex;
}

.results-pick p {
  font-size: 1rem;
  margin-top: 2rem;
  letter-spacing: 1px;
}

.rules-trigger {
  position: absolute;
  bottom: 1rem;
  right: 1rem;
}

.score-board {
  align-self: stretch;
  border-radius: var(--border-radius);
  background-color: #fff;
  margin-left: auto;
  text-align: center;
  color: black;
  display: flex;
  align-items: center;
  padding: 0 2rem;
}

.score-board h2 {
  color: var(--score-text);
  font-size: 0.8rem;
  font-weight: normal;
  line-height: 1;
}

.score-board .score {
  color: var(--dark-text);
  font-size: 2rem;
}

@media (min-width: 1024px) {
  main {
    width: calc(100% - 30px);
    max-width: 100%;
  }

  .results {
    margin-top: 0;
    text-align: center;
  }

  .results button {
    display: inline-flex;
  }

  .results-grid {
    align-items: center;
    grid-template-columns: 1fr 4fr 1fr;
  }

  h1 {
    font-size: 1.5rem;
  }
}
</style>
