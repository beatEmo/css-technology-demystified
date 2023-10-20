<template>
  <div class="native-container">
    <div
      class="cube"
      :style="{
        '--length': length,
        '--degOut': degOut,
        '--degIn': degIn,
        '--angle': angle
      }"
    >
      <span
        v-for="(item, index) of data"
        :key="index"
        :style="{ '--i': index, backgroundColor: item.color }"
        >{{ item.num }}</span
      >
    </div>
  </div>
</template>

<script>
export default {
  name: "spriteCube",
  data() {
    return {
      data: [
        { num: 1, color: "red" },
        { num: 2, color: "green" },
        { num: 3, color: "skyblue" },
        { num: 4, color: "pink" }
      ],
      angle: 0,
      degOut: 0,
      degIn: 0,
      length: 0,
      node: null,
      startX: 0,
      endX: 0,
      moveX: 0,
      index: 0,
      NOde: null
    };
  },
  mounted() {
    // this.a();
    this.node = document.querySelector(".native-container");
    this.node.addEventListener("touchstart", this.touchStart);
    this.node.addEventListener("touchmove", this.touchMove);
    this.node.addEventListener("touchend", this.touchEnd);

    document.querySelector(".cube").addEventListener("transitionend", () => {
      console.log(1111);
    });
  },
  methods: {
    touchStart(e) {
      this.startX = e.touches[0].screenX;
    },
    touchMove(e) {
      document.querySelector(".cube").style.transition = "1s transform";
      this.endX = e.changedTouches[0].screenX;
      this.moveX = this.endX - this.startX;
      if (this.moveX > 0) {
        // xia -
      } else {
        // zuo
        // document.querySelector(".cube").children[0].classList.add("active");
        // document.querySelector(".cube").children[1].style.transform =
        //   " translate(0) scale(1)";
      }
    },
    touchEnd() {
      if (this.moveX > 0) {
        //
      } else {
        if (this.index == 0) {
          this.NOde = document.querySelector(".cube").cloneNode(true);
        }
        //
        document.querySelector(".cube").children[this.index].style.transform =
          " translate(-105%)";
        document.querySelector(".cube").children[
          this.index + 1
        ].style.transform = " translate(0) scale(1)";
        document.querySelector(".cube").children[
          this.index + 2
        ].style.transform = "  translate(15%) scale(0.9)";

        this.index++;
        if (this.index % 4 > 1) {
          for (const item of Array.from(this.NOde.children))
            document.querySelector(".cube").appendChild(item);
        }
      }
    },
    a() {
      const nodes = Array.from(document.querySelector(".cube").children);
      nodes.forEach((item, index) => {
        if (index == 0) {
          item.className = "a";
        }
        if (index == 1) {
          item.className = "b";
        }
        if (index == 2) {
          item.className = "b";
        }
      });
    }
  }
};
</script>
<style lang="scss">
body,
html {
  padding: 0;
  margin: 0;
}
* {
  box-sizing: border-box;
}
</style>
<style lang="scss" scoped>
/* .native-container:hover > .cube {
  transform: rotateX(360deg);
} */
.active {
  animation: 1s move cubic-bezier(0, 0, 1, 0.5);
}
@keyframes move {
  0% {
    transform: translate(0);
  }
  50% {
    transform: translate(-110%);
  }
  100% {
    transform: translate(30%) scale(0.8);
  }
}
.native-container {
  width: 100vw;
  height: 100vh;
  overflow-y: auto;
  perspective: 800px;
  display: flex;
  justify-content: center;
  border: 1px solid #000;
  .cube {
    width: calc(100% - 20px);
    height: 216px;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;

    & > span {
      position: absolute;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;
      transition: all 0.6s;
      text-align: center;
      font: 50px/300px "微软雅黑";
      backface-visibility: hidden;
      width: 80%;
      transform: translate(30%) scale(0.8);
      z-index: var(--i);
      &:nth-child(1) {
        /* z-index: 9 !important;
        transform: translate(0) !important; */
        z-index: 9;
        transform: translate(0);
      }
      &:nth-child(2) {
        /* background: skyblue; */
        /* z-index: 8 !important;
        transform: translate(15%) scale(0.9) !important; */
        z-index: 8;
        transform: translate(15%) scale(0.9);
      }
      &:nth-child(3) {
        /* background: pink; */
        /* z-index: 7 !important;
        transform: translate(30%) scale(0.8) !important; */
        z-index: 7;
        transform: translate(30%) scale(0.8);
      }
    }
  }
}
</style>
