<template>
  <div class="main">
    <div class="box">Remaining Attempts: {{ attemptsRemaining }}/3</div>
    <div class="box">Health: {{ displayHealth }}</div>
    <div class="box">Ability Points: {{ abilityPoints }}</div>
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
          <td><PlusButton /></td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
        </tr>
        <tr>
          <td>Normal</td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
        </tr>
        <tr>
          <td>Slow</td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
          <td><PlusButton /></td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
import PlusButton from "./plusButton.vue";

export default {
  components: {
    PlusButton,
  },
  data() {
    return {
      attempts: 3,
      abilityPoints: 0,
      displayHealth: "♥ ♥ ♥",
    };
  },
  props: {
    attemptsRemaining: Number,
    health: Number,
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
};
</script>

<style scoped>
.main {
  background-color: white;
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
</style>
