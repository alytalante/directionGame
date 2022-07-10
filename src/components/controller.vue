<template>
  <Conductor
    :speed="this.speed"
    :stack="this.stack"
    :scoreArray="this.scoreArray"
    @turn="
      (i) => {
        passUpEmit(i);
      }
    "
  />
  <div class="Flex">
    <ArrowBox displayIcon="←" />
    <ArrowBox displayIcon="↑" />
    <ArrowBox displayIcon="→" />
  </div>
</template>

<script>
import ArrowBox from "./arrowBox.vue";
import Conductor from "./conductor.vue";

export default {
  components: {
    ArrowBox,
    Conductor,
  },
  emits: ["turn"],
  props: {
    stack: Number,
    speed: Number,
    scoreArray: Array,
  },
  watch: {
    scoreArray(newValue) {
      console.log(newValue);
    },
  },
  methods: {
    passUpEmit(i) {
      this.$emit("turn", i);
    },
  },
};
</script>

<style>
body {
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #191919;
  height: 100vh;
  padding-top: 20px;
}
.Flex {
  background-color: #ededed;
  display: flex;
  border: 1px solid black;
  width: 200px;
  justify-content: space-between;
  padding: 10px;
  margin: 0 auto;
}
</style>
