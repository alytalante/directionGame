<template>
  <div class="main">
    <div class="attack" @click="$emit('attack', fastAttack)">
      <strong>Fast Attack:</strong>

      {{ fastAttack.speed / 1000 }}s, {{ fastAttack.stack }},
      {{ fastAttack.scoreArray }}
    </div>
    <div class="attack" @click="$emit('attack', normalAttack)">
      <strong>Normal Attack:</strong>
      {{ normalAttack.speed / 1000 }}s, {{ normalAttack.stack }},
      {{ normalAttack.scoreArray }}
    </div>
    <div class="attack" @click="$emit('attack', slowAttack)">
      <strong>Slow Attack:</strong>
      {{ slowAttack.speed / 1000 }}s, {{ slowAttack.stack }},
      {{ slowAttack.scoreArray }}
    </div>
  </div>
</template>
<script>
export default {
  props: {
    skillChange: Object,
  },
  data() {
    return {
      fastAttack: {
        speed: 600,
        stack: 15,
        scoreArray: [1, 5, 11],
      },
      normalAttack: {
        stack: 10,
        speed: 1000,
        scoreArray: [1, 2, 6],
      },
      slowAttack: {
        stack: 15,
        speed: 1200,
        scoreArray: [1, 2, 4],
      },
    };
  },
  watch: {
    skillChange(newValue) {
      if (newValue.status === "FS") {
        this.fastAttack.stack++;
      } else if (newValue.status === "F1") {
        this.fastAttack.scoreArray[0]++;
      } else if (newValue.status === "F2") {
        this.fastAttack.scoreArray[1]++;
      } else if (newValue.status === "F3") {
        this.fastAttack.scoreArray[2]++;
      } else if (newValue.status === "NS") {
        this.normalAttack.stack++;
      } else if (newValue.status === "N1") {
        this.normalAttack.scoreArray[0]++;
      } else if (newValue.status === "N2") {
        this.normalAttack.scoreArray[1]++;
      } else if (newValue.status === "N3") {
        this.normalAttack.scoreArray[2]++;
      } else if (newValue.status === "SS") {
        this.slowAttack.stack++;
      } else if (newValue.status === "S1") {
        this.slowAttack.scoreArray[0]++;
      } else if (newValue.status === "S2") {
        this.slowAttack.scoreArray[1]++;
      } else if (newValue.status === "S3") {
        this.slowAttack.scoreArray[2]++;
      }
    },
  },
};
</script>

<style scoped>
.main {
  display: flex;
  flex-direction: column;
  background-color: white;
  border: 1px solid black;
  border-right: 0px;
  border-bottom: 0;
  width: 220px;
}
.attack {
  border-bottom: 1px solid black;
  flex: 1;
  cursor: pointer;
  display: grid;
  align-items: center;
}

.attack:hover {
  border-bottom: 1px solid black;
  flex: 1;
  cursor: pointer;
  display: grid;
  align-items: center;
  background-color: lightskyblue;
}
</style>
