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
