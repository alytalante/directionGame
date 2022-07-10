<template>
  <div class="main">
    <div class="box">
      <strong>Remaining Attempts: </strong>{{ attemptsRemaining }}/3
    </div>
    <div class="box">
      <strong>Health: </strong><span class="health">{{ displayHealth }}</span>
    </div>
    <div class="box"><strong>Ability Points: </strong>{{ abilityPoints }}</div>
    <div class="Upgrades box">
      <table>
        <tr>
          <td></td>
          <td>Stack</td>
          <td>1</td>
          <td>2</td>
          <td>3</td>
        </tr>
        <tr>
          <td>Fast</td>
          <td><PlusButton @click="spendPoints('FS')" /></td>
          <td><PlusButton @click="spendPoints('F1')" /></td>
          <td><PlusButton @click="spendPoints('F2')" /></td>
          <td><PlusButton @click="spendPoints('F3')" /></td>
        </tr>
        <tr>
          <td>Normal</td>
          <td><PlusButton @click="spendPoints('NS')" /></td>
          <td><PlusButton @click="spendPoints('N1')" /></td>
          <td><PlusButton @click="spendPoints('N2')" /></td>
          <td><PlusButton @click="spendPoints('N3')" /></td>
        </tr>
        <tr>
          <td>Slow</td>
          <td><PlusButton @click="spendPoints('SS')" /></td>
          <td><PlusButton @click="spendPoints('S1')" /></td>
          <td><PlusButton @click="spendPoints('S2')" /></td>
          <td><PlusButton @click="spendPoints('S3')" /></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import PlusButton from "./plusButton.vue";

export default {
  emits: ["skillUp"],
  components: {
    PlusButton,
  },
  data() {
    return {
      attempts: 3,
      displayHealth: "♥ ♥ ♥",
    };
  },
  props: {
    attemptsRemaining: Number,
    health: Number,
    abilityPoints: Number,
  },
  watch: {
    health(newValue) {
      if (newValue === 2) {
        this.displayHealth = "♥ ♥";
      } else if (newValue === 1) {
        this.displayHealth = "♥";
      } else if (newValue === 0) {
        this.displayHealth = "";
      }
    },
  },
  methods: {
    spendPoints(skill) {
      if (this.abilityPoints > 0) {
        this.$emit("skillUp", skill);
      }
    },
  },
};
</script>

<style scoped>
.main {
  background-color: #ededed;
  border: 1px solid black;
  border-top: 0;
  border-left: 0px;
  width: 220px;
  display: flex;
  flex-direction: column;
}
.Upgrades {
  text-align: left;
}

table {
  width: 95%;
  border-collapse: collapse;
  margin: 2px auto;
}

th,
td {
  border: 1px solid black;
}
.box {
  display: grid;
  place-items: center;
  flex: 1;
  border-top: 1px solid black;
}
.health {
  color: #8685ef;
  display: inline;
}
</style>
