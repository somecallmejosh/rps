<template>
  <div>
    <header>
      <h1>Rock Paper Scissors</h1>
      <div class="score-board">
        <div>
          <h2>Score</h2>
          <span class="score">12</span>
        </div>
      </div>
    </header>
    <nuxt />
  </div>
</template>

<style>
header {
  border: #fff 1px solid;
  border-radius: 2rem;
  display: grid;
  grid-template-columns: 1fr 1fr;
  padding: 1rem;
}
h1 {
  max-width: 100px;
}
.score-board {
  border-radius: 12px;
  background-color: #fff;
  margin-left: auto;
  text-align: center;
  color: black;
  display: flex;
  align-items: center;
  padding: 0 2rem;
}
</style>
