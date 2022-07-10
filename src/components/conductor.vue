<template>
  <div class="info">
    <div class="infoBox">
      <strong> Time: </strong>
      {{ speed / 1000 }}s
    </div>
    <div class="infoBox">
      <strong>Stack:</strong>
      {{ remainingStack }}
    </div>
  </div>
  <div class="timeBox">
    <div
      class="time"
      :style="{
        width: `${this.time / this.divisor}px`,
        background: timerColor,
      }"
    ></div>
  </div>

  <div
    v-if="!isGameOver"
    :class="{ box: isUnpressed, boxPressed: !isUnpressed }"
  >
    <div v-if="!openingPlay">
      {{ icon }}
    </div>
    <div class="enter" v-if="openingPlay">
      Press <br />
      Enter <br />
      To<br />
      Begin
    </div>
  </div>
  <div
    v-if="isGameOver"
    :class="{ box: isUnpressed, boxPressed: !isUnpressed }"
  >
    <div>
      {{ parseInt(score) }}
    </div>
  </div>
</template>

<script>
export default {
  emits: ["turn"],
  props: {
    stack: Number,
    speed: Number,
    scoreArray: Array,
  },

  data() {
    return {
      openingPlay: true,
      divisor: null,
      remainingStack: null,
      scoreIncrament: 1,
      isKeyPressed: false,
      isUnpressed: true,
      icon: null,
      time: 1000,
      isGameOver: false,
      score: 0,
      timerColor: "#3A586E",
      timer: null,
    };
  },
  watch: {
    time(newValue) {
      if (newValue < 1) {
        this.isGameOver = true;
      }

      const uppLimit = this.speed + 1;
      const firstMarker = uppLimit * 0.675;
      const secondMarker = uppLimit * 0.4;

      if (newValue < uppLimit && newValue > firstMarker) {
        this.scoreIncrament = this.scoreArray[2];
        this.timerColor = "#3A586E";
      } else if (newValue < firstMarker + 1 && newValue > secondMarker) {
        this.scoreIncrament = this.scoreArray[1];
        this.timerColor = "#23A7B8";
      } else {
        this.scoreIncrament = this.scoreArray[0];
        this.timerColor = "#65FBD2";
      }
    },
    remainingStack(newValue) {
      if (newValue === 0) {
        this.isGameOver = true;
      }
    },
    stack(newValue) {
      this.remainingStack = this.stack;
    },
    isGameOver(newValue) {
      if (newValue === true) {
        console.log("TURN DATA SENT");
        this.$emit("turn", { score: this.score });
      }
    },
  },
  methods: {
    determineTimeDivision(time) {
      const division = time / 220;
      this.divisor = division;
    },
    resetTimer() {
      this.time = this.speed;
      clearInterval(this.timer);
      this.timer = setInterval(() => {
        if (this.time > 0) {
          this.time = this.time - 100;
        }
      }, 100);
    },
    changeIcon() {
      this.resetTimer();

      //actually reassign icon
      const icons = ["←", "↑", "→"];
      let rng = Math.floor(Math.random() * 3);
      this.icon = icons[rng];

      if (this.openingPlay === false) {
        this.increaseScore();
      }
    },
    increaseScore() {
      if (this.isGameOver === false) {
        this.score = this.score + this.scoreIncrament;
        this.remainingStack = this.remainingStack - 1;
      }
    },
    reset() {
      this.remainingStack = this.stack;
      clearInterval(this.timer);

      this.divisor = null;
      this.scoreIncrament = 1;
      this.isKeyPressed = false;
      this.isUnpressed = true;

      this.time = 1000;
      this.isGameOver = false;
      this.score = 0;
      this.timerColor = "#20B2AA";
      this.timer = null;

      this.icon = "Press Enter";
      this.determineTimeDivision(this.speed);
      this.time = this.speed;
      this.openingPlay = true;
    },
    checkInput(key) {
      if (this.icon === "←" && (key === "a" || key === "ArrowLeft")) {
        this.isUnpressed = false;
        setTimeout(() => {
          this.isUnpressed = true;
        }, 100);
        this.changeIcon();
      } else if (this.icon === "→" && (key === "d" || key === "ArrowRight")) {
        this.isUnpressed = false;
        setTimeout(() => {
          this.isUnpressed = true;
        }, 100);
        this.changeIcon();
      } else if (this.icon === "↑" && (key === "w" || key === "ArrowUp")) {
        this.isUnpressed = false;
        setTimeout(() => {
          this.isUnpressed = true;
        }, 100);
        this.changeIcon();
      } else if (
        key === "w" ||
        key === "ArrowUp" ||
        key === "a" ||
        key === "ArrowLeft" ||
        key === "d" ||
        key === "ArrowRight"
      ) {
        this.isGameOver = true;
      }
    },
  },
  created() {
    this.icon = "Press Enter";
    this.determineTimeDivision(this.speed);
    this.time = this.speed;
    this.remainingStack = this.stack;

    window.addEventListener("keydown", (e) => {
      if (e.key === "Enter") {
        if (!this.isGameOver && this.openingPlay) {
          this.changeIcon();
          this.openingPlay = false;
        } else if (this.isGameOver) {
          this.reset();
        }
      }
      if (
        this.openingPlay === false &&
        this.isGameOver === false &&
        (e.key == "d" ||
          e.key == "ArrowRight" ||
          e.key == "a" ||
          e.key == "w" ||
          e.key == "ArrowLeft" ||
          e.key == "ArrowUp")
      ) {
        if (this.isKeyPressed === false) {
          this.checkInput(e.key);
        }
        this.isKeyPressed = true;
      }
      window.addEventListener("keyup", (e) => {
        if (
          e.key == "d" ||
          e.key == "ArrowRight" ||
          e.key == "a" ||
          e.key == "w" ||
          e.key == "ArrowLeft" ||
          e.key == "ArrowUp"
        ) {
          this.isKeyPressed = false;
        }
      });
    });
  },
};
</script>

<style scoped>
.box {
  background-color: #ededed;
  border: 1px solid black;
  width: 50px;
  height: 220px;
  width: 220px;
  font-size: 5rem;
  display: grid;
  margin: 0 auto;
  align-items: center;
  border-bottom: 0;
  margin-top: 0;
}
.boxPressed {
  border: 1px solid black;
  width: 50px;
  height: 220px;
  width: 220px;
  font-size: 5rem;
  display: grid;
  margin: 0 auto;
  margin-top: 0;
  align-items: center;
  border-bottom: 0;
  background-color: #d3fbd8;
}
.time {
  margin: 0 auto;
  height: 10px;
}

.timeBox {
  background-color: #ededed;
  border: 1px solid #000000;
  border-bottom: 0;
  width: 220px;
  margin: 0 auto;
}

.info {
  background-color: #ededed;
  width: 220px;
  margin: 0 auto;
  border: 1px solid black;
  border-bottom: 0;
  display: flex;
  justify-content: space-evenly;
  padding: 5px 0 5px 0;
}

.infoBox {
  width: 110px;
}
.enter {
  font-weight: bold;
  font-size: 2.3rem;
  line-height: 2.3rem;
}
</style>
