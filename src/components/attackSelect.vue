<template>
  <div class="main">
    <div class="attack" @click="$emit('attack', fastAttack)">
      <strong>Fast Attack:</strong>
      <table>
        <tr>
          <td>Time</td>
          <td>Stack</td>
          <td>Mod</td>
        </tr>
        <tr>
          <td>{{ fastAttack.speed / 1000 }}s</td>
          <td>{{ fastAttack.stack }}</td>
          <td class="mod">
            <div class="ok">{{ fastAttack.scoreArray[0] }}</div>
            <div class="good">{{ fastAttack.scoreArray[1] }}</div>
            <div class="perfect">{{ fastAttack.scoreArray[2] }}</div>
          </td>
        </tr>
      </table>
    </div>
    <div class="attack" @click="$emit('attack', normalAttack)">
      <strong>Normal Attack:</strong>
      <table>
        <tr>
          <td>Time</td>
          <td>Stack</td>
          <td>Mod</td>
        </tr>
        <tr>
          <td>{{ normalAttack.speed / 1000 }}s</td>
          <td>{{ normalAttack.stack }}</td>
          <td class="mod">
            <div class="ok">{{ normalAttack.scoreArray[0] }}</div>
            <div class="good">{{ normalAttack.scoreArray[1] }}</div>
            <div class="perfect">{{ normalAttack.scoreArray[2] }}</div>
          </td>
        </tr>
      </table>
    </div>
    <div class="attack" @click="$emit('attack', slowAttack)">
      <strong>Slow Attack:</strong>
      <table>
        <tr>
          <td>Time</td>
          <td>Stack</td>
          <td>Mod</td>
        </tr>
        <tr>
          <td>{{ slowAttack.speed / 1000 }}s</td>
          <td>{{ slowAttack.stack }}</td>
          <td class="mod">
            <div class="ok">{{ slowAttack.scoreArray[0] }}</div>
            <div class="good">{{ slowAttack.scoreArray[1] }}</div>
            <div class="perfect">{{ slowAttack.scoreArray[2] }}</div>
          </td>
        </tr>
      </table>
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
  background-color: #ededed;
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
  background-color: #aca7cb;
}

.statFlex {
  display: flex;
}
.stat {
  flex: 1;
  border: 1px solid black;
}

.mod {
  display: flex;
  border: none;
}

.ok {
  background-color: #65fbd2;
  flex: 1;
}

.good {
  background-color: #23a7b8;
  flex: 1;
}
.perfect {
  color: #ededed;
  background-color: #3a586e;
  flex: 1;
}

table {
  background-color: #ededed;
  border-collapse: collapse;
  margin: 0 3px 0 3px;
}

tr,
td {
  border: 1px solid black;
}
</style>
