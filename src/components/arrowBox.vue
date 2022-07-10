<template>
  <div :class="{ box: isUnpressed, boxPressed: !isUnpressed }">
    {{ displayIcon }}
  </div>
</template>

<script>
export default {
  data() {
    return {
      isUnpressed: true,
    };
  },
  props: {
    displayIcon: "",
  },
  created() {
    if (this.displayIcon === "←") {
      window.addEventListener("keydown", (e) => {
        if (e.key == "a" || e.key == "ArrowLeft") {
          if (this.isUnpressed === true) {
          }
          this.isUnpressed = false;
        }
      });
      window.addEventListener("keyup", (e) => {
        if (e.key == "a" || e.key == "ArrowLeft") {
          this.isUnpressed = true;
        }
      });
    } else if (this.displayIcon === "↑") {
      window.addEventListener("keydown", (e) => {
        if (e.key == "w" || e.key == "ArrowUp") {
          if (this.isUnpressed === true) {
          }
          this.isUnpressed = false;
        }
        window.addEventListener("keyup", (e) => {
          if (e.key == "w" || e.key == "ArrowUp") {
            this.isUnpressed = true;
          }
        });
      });
    } else if (this.displayIcon === "→") {
      window.addEventListener("keydown", (e) => {
        if (e.key == "d" || e.key == "ArrowRight") {
          if (this.isUnpressed === true) {
          }
          this.isUnpressed = false;
        }
        window.addEventListener("keyup", (e) => {
          if (e.key == "d" || e.key == "ArrowRight") {
            this.isUnpressed = true;
          }
        });
      });
    }
  },
  methods: {
    handleKeyPress() {
      console.log("test");
    },
  },
};
</script>

<style scoped>
.box {
  border: 1px solid black;
  height: 50px;
  width: 50px;
  font-size: 2rem;
  background-color: white;
}

.boxPressed {
  border: 1px solid black;
  height: 50px;
  width: 50px;
  font-size: 2rem;
  background-color: lightcoral;
}
</style>
