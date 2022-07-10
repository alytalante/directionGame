<template>
  <div class="levelBox">
    <h2>
      <strong>Level {{ level }}</strong>
    </h2>
  </div>
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
      :skillChange="skillChange"
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
    <CurrentLevel
      :attemptsRemaining="attemptsRemaining"
      :health="health"
      :abilityPoints="abilityPoints"
      @skillUp="
        (i) => {
          handleSkillUp(i);
        }
      "
    />
  </div>
</template>

<script>
import Controller from "./components/controller";
import AttackSelect from "./components/attackSelect.vue";
import CurrentLevel from "./components/currentLevel.vue";
import EnemyBox from "./components/enemyBox.vue";

export default {
  emits: ["fail", "success", "skillUp"],
  components: {
    Controller,
    AttackSelect,
    CurrentLevel,
    EnemyBox,
  },
  data() {
    return {
      level: 1,
      stack: 10,
      speed: 1000,
      scoreArray: [1, 2, 6.5],
      score: 0,
      attemptsRemaining: 3,
      abilityPoints: 0,
      health: 3,
      skillChange: null,
    };
  },
  watch: {
    level(newValue) {
      if (newValue % 2 === 0) {
        this.abilityPoints++;
      }
    },
  },
  methods: {
    registerAttackSelection(attack) {
      this.stack = attack.stack;
      this.speed = attack.speed;
      this.scoreArray = attack.scoreArray;
    },
    endTurn(i) {
      const smallRng = Math.random() / 100;
      this.score = i.score + smallRng;
      console.log("TURN DATA RECIEVED");
      console.log(i);
      console.log(this.attemptsRemaining);
      this.attemptsRemaining = this.attemptsRemaining - 1;
    },
    handleFail(i) {
      this.health = this.health - 1;
      if (this.health > 0) {
        this.attemptsRemaining = 3;
      }
    },
    handleSuccess(i) {
      this.level++;
      this.attemptsRemaining = 3;
    },
    handleSkillUp(i) {
      this.abilityPoints = this.abilityPoints - 1;
      this.skillChange = {
        status: i,
      };
    },
  },
};
</script>

<style scoped>
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
.appFlex {
  display: flex;
  justify-content: center;
  gap: 2px;
  margin-top: 2px;
}
.levelBox {
  background-color: #ededed;
  max-width: 666px;
  margin: 2px auto;
  border: 1px solid black;
}
h2 {
  font-weight: bolder;
  margin: 4px;
}
</style>
