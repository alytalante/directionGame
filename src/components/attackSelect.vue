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
        scoreArray: [1, 2, 6.5],
      },
      slowAttack: {
        stack: 15,
        speed: 1200,
        scoreArray: [1, 2, 4],
      },
    };
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
