<template>
  <div class="flex one">
    <div class="enemyBox one">
      <div>
        <strong>Par:</strong>
        <br />
        {{ par }}
      </div>
    </div>
    <div class="enemyBox two">
      <img :src="levelOneMonsters[lvl1Rng]" />
    </div>
    <div class="enemyBox three">
      <div>
        <strong> Total: </strong>
        <br />
        {{ total }}
      </div>
    </div>
  </div>
</template>

<script>
import bat from "../assets/bat.png";
import crow from "../assets/crow.png";
import snake from "../assets/snake.png";
import flame from "../assets/flame.png";
import fire from "../assets/fire.png";

export default {
  emits: ["fail", "success"],
  data() {
    return {
      levelOneMonsters: [bat, crow, snake, flame, fire],
      lvl1Rng: Math.floor(Math.random() * (4 - 0 + 1)) + 0,
      total: 0,
      par: 0,
      dificultyModifier: 1,
    };
  },
  props: {
    attemptsRemaining: Number,
    incomingScore: Number,
  },
  watch: {
    incomingScore(newValue) {
      if (this.attemptsRemaining !== -1) {
        console.log("Incoming SCORE RECIEVED");
        this.total = this.total + parseInt(this.incomingScore);
      }
    },
    attemptsRemaining(newValue) {
      if (newValue === 0) {
        if (this.total > this.par) {
          this.dificultyModifier = this.dificultyModifier + 0.14;
          this.$emit("success", { status: "success" });
          setTimeout(() => {
            this.total = 0;
            this.generatePar();
            this.lvl1Rng = Math.floor(Math.random() * (4 - 0 + 1)) + 0;
          }, 1500);
        }
        if (this.total < this.par) {
          this.$emit("fail", { status: "failure" });
          setTimeout(() => {
            this.total = 0;
          }, 1500);
        }
      }
    },
  },
  methods: {
    generatePar() {
      const min = 100;
      const max = 115;
      const beforemultiplier =
        Math.floor(Math.random() * (max - min + 1)) + min;
      this.par = parseInt(beforemultiplier * this.dificultyModifier);
    },
  },
  created() {
    this.generatePar();
  },
};
</script>

<style>
.enemyBox {
  background-color: #ededed;
  width: 220px;
  height: 200px;
  border: 1px solid black;
  display: grid;
  align-items: center;
  place-items: center;
  justify-content: center;
  justify-items: center;

  border-bottom: 0;
}
.enemyBox img {
  display: block;
}

.one {
  font-size: 3rem;
}

.two {
  border-left: 0;
  border-right: 0;
}

.flex {
  display: flex;
  justify-content: center;
  gap: 2px;
}

img {
  max-width: 95%;
}
</style>
