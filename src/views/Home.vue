<template>
  <div class="counter">
    <Counter
      :year="2020"
      :month="11"
      :date="31"
      :hour="23"
      :minute="59"
      :second="59"
      :millisecond="31"
    />
  </div>
</template>

<script>
import Counter from "../components/Counter";
export default {
  components: {
    Counter
  }
};
</script>

<style scoped>
.counter {
  padding: 2em 4em;
  display: flex;
  justify-content: center;
  align-content: center;
}
</style>