<template>
  <EnemyBox
    :incomingScore="score"
    :attemptsRemaining="attemptsRemaining"
    @fail="
      (i) => {
        handleFail(i);
      }
    "
    @success="
      (i) => {
        handleSuccess(i);
      }
    "
  />
  <div class="appFlex">
    <AttackSelect
      @attack="
        (i) => {
          this.registerAttackSelection(i);
        }
      "
    />
    <div>
      <Controller
        :stack="stack"
        :speed="speed"
        :scoreArray="scoreArray"
        @turn="
          (i) => {
            endTurn(i);
          }
        "
      />
    </div>
    <CurrentLevel :attemptsRemaining="attemptsRemaining" :health="health" />
  </div>
</template>

<script>
import Controller from "./components/controller";
import AttackSelect from "./components/attackSelect.vue";
import CurrentLevel from "./components/currentLevel.vue";
import EnemyBox from "./components/enemyBox.vue";

export default {
  emits: ["fail", "success"],
  components: {
    Controller,
    AttackSelect,
    CurrentLevel,
    EnemyBox,
  },
  data() {
    return {
      stack: 10,
      speed: 1000,
      scoreArray: [1, 2, 6.5],
      score: 0,
      attemptsRemaining: 3,
      health: 3,
    };
  },
  methods: {
    registerAttackSelection(attack) {
      this.stack = attack.stack;
      this.speed = attack.speed;
      this.scoreArray = attack.scoreArray;
    },
    endTurn(i) {
      console.log("TURN DATA RECIEVED");
      console.log(i);
      console.log(this.attemptsRemaining);
      this.score = i.score;
      this.attemptsRemaining = this.attemptsRemaining - 1;
    },
    handleFail(i) {
      this.health = this.health - 1;
      if (this.health > 0) {
        this.attemptsRemaining = 3;
      }
    },
    handleSuccess(i) {
      this.attemptsRemaining = 3;
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
  background-color: white;
  display: flex;
  border: 1px solid black;
  width: 200px;
  justify-content: space-between;
  padding: 10px;
  margin: 0 auto;
}
.appFlex {
  display: flex;
  justify-content: center;
  gap: 2px;
  margin-top: 2px;
}
</style>
