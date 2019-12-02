<template>
  <section class="wrapper">
    <div>
      <selection option="rock" />
      <selection option="paper" />
      <selection option="scissors" />
    </div>
    <div>
      <selection option="rock" state="disabled" />
      <selection option="paper" state="disabled" />
      <selection option="scissors" state="disabled" />
    </div>
  </section>
</template>

<script>
import Selection from "~/components/Selection.vue";
export default {
  components: { Selection }
};
</script>

<style>
.wrapper {
  display: flex;
}

button {
  margin: 2rem;
}
</style>
