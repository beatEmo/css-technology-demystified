<template>
  <div class="app">
    <div class="container">
      <div class="cube" ref="cube">
        <span :style="{ '--i': 0, 'background-color': 'aqua' }">1</span>
        <span :style="{ '--i': 1, 'background-color': 'red' }">2</span>
        <span :style="{ '--i': 2, 'background-color': 'pink' }">3</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      top: 0,
      aaa: 0,
      angle: 0
    };
  },
  mounted() {
    this.top = document.querySelector(".container").getBoundingClientRect().top;
    setInterval(() => {
      this.$refs.cube.style.transition = "none";
      const top = document
        .querySelector(".container")
        .getBoundingClientRect().top;
      const moveY = this.top - top;
      if (top == this.aaa) {
        this.$refs.cube.style.transition = "transform .5s";
        this.top = top;
        this.angle = this.angle + Math.round(moveY / 216) * 120;
        this.$refs.cube.style.transform = `rotateX(${this.angle}deg)`;
        return;
      }
      this.aaa = top;
      console.log(moveY, this.top);
      const angle = this.angle + (moveY / 216) * 120;
      if (moveY < 0) {
        // xia
        this.$refs.cube.style.transform = `rotateX(${angle}deg) scale(.9)`;
      } else {
        // shang
        this.$refs.cube.style.transform = `rotateX(${angle}deg)`;
      }
    }, 100);
    // const node = document.querySelector(".container");
    // let startY = 0;
    // let endY = 0;
    // let d = 0;
    // node.addEventListener("touchstart", (e) => {
    //   this.$refs.cube.style.transition = ``;
    //   startY = e.touches[0].screenY;
    // });
    // node.addEventListener("touchmove", (e) => {
    //   endY = e.touches[0].screenY;
    //   d = endY - startY;
    //   const top = this.top + d;
    //   if (top < 0 && top > window.innerHeight - 216) return;
    //   const x = (d * 360) / window.innerHeight;
    //   const angle = this.angle + x;
    //   console.log(this.angle, "---------");
    //   this.$refs.cube.style.transform = `rotateX(${-angle}deg)`;
    // });
    // node.addEventListener("touchend", () => {
    //   const x = (d * 360) / window.innerHeight;
    //   const m = Math.round(x / 120) * 120;
    //   this.angle = this.angle + m;
    //   console.log(this.angle, "===========");
    //   this.$refs.cube.style.transform = `rotateX(${-this.angle}deg)`;
    //   this.$refs.cube.style.transition = `transform 0.4s cubic-bezier(0, 0.3, 1, 0.67)`;
    // });
  },
  methods: {
    getTop() {
      const top = this.$refs.cube.getBoundingClientRect().top;
      console.log(top);
      if (top < 0 && top > window.innerHeight - 216) return;
    }
  }
};
</script>

<style scoped>
.app {
  width: 100vw;
  height: 1000px;
  padding-top: 700px;
}
.container {
  width: 100vw;
  height: 216px;
  perspective: 800px;
}
.cube {
  width: calc(100% -20px);
  height: 216px;
  display: flex;
  justify-content: center;
  position: relative;
  transform-origin: center center -62px;
  transform-style: preserve-3d;
  /* transition: transform 0.5s cubic-bezier(0, 0.3, 1, 0.67); */
}
.cube > span {
  position: absolute;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  transform-origin: center center -62px;
  transform: rotateX(calc(var(--i) * 120deg));
}
</style>
