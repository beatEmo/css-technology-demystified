<template>
  <div class="native-container">
    <div class="cube">
      <span
        :class="{
          left: index === current % data.length,
          center: index === (current + 1) % data.length,
          right: index === (current + 2) % data.length
        }"
        v-for="(item, index) of data"
        :key="index"
        :style="{ backgroundColor: item.color }"
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
        { num: 3, color: "skyblue" }
        // { num: 4, color: "pink" }
      ],
      current: 0,
      transitionFlag: true,
      // 展示三个面
      isShowM: 3,
      styleEL: [
        {
          transform: "translate(-110%, -50%)"
        },
        {
          transform: "translate(0,-50%)",
          height: "100%"
          // zIndex: "-1"
        },
        {
          transform: "translate(12.5%,-50%)",
          height: "90%"
          // zIndex: "-1"
        }
      ]
    };
  },
  mounted() {
    this.node = document.querySelector(".native-container > .cube");
    this.node.addEventListener("touchstart", this.touchStart);
    this.node.addEventListener("touchmove", this.touchMove);
    this.node.addEventListener("touchend", this.touchEnd);
  },
  methods: {
    touchStart(e) {
      this.startX = e.touches[0].screenX;
    },
    touchMove(e) {
      this.endX = e.changedTouches[0].screenX;
      this.moveX = this.endX - this.startX;
      if (this.moveX > 0) {
        console.log(111);
      } else {
        // zuo
      }
    },
    async touchEnd() {
      if (this.moveX > 0) {
        //
      } else {
        //
        console.log(111);
        this.transitionFlag = true;
        for (let i = this.isShowM - 1; i > -1; i--) {
          const index = (this.current + i) % this.data.length;
          for (let atrr in this.styleEL[i]) {
            console.log(this.node.children[index]);
            this.node.children[index].style[atrr] = this.styleEL[i][atrr];
          }
        }

        this.node.children[this.current % this.data.length].addEventListener(
          "transitionend",
          this.move
        );
      }
    },
    move() {
      if (!this.transitionFlag) return;
      console.log(this.current);

      for (let i = this.isShowM - 1; i > -1; i--) {
        const index = (this.current + i) % this.data.length;
        for (let atrr in this.styleEL[i]) {
          console.log(this.node.children[index]);
          this.node.children[index].style[atrr] = "";
        }
      }
      this.current++;
      this.transitionFlag = false;
      if (this.current > this.data.length - 1) {
        this.current = 0;
      }
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
.native-container {
  width: 100vw;
  height: 100vh;
  overflow-y: auto;
  perspective: 800px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #000;
  perspective: 800px;
  .cube {
    display: flex;
    align-items: center;
    width: calc(100% - 20px);
    height: 216px;
    position: relative;
    border: 1px solid #000;
    transform-style: preserve-3d;
    /* left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto; */
    overflow: hidden;
    & > span {
      display: flex;
      transition: all 0.4s;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;
      text-align: center;
      font: 50px/300px "微软雅黑";
      backface-visibility: hidden;

      width: 80%;
      position: absolute;
      margin: auto;
      z-index: -1;
      top: 50%;
      transform: translateY(-50%);
      left: 0;
      visibility: hidden;
      height: 100%;

      &.left {
        visibility: visible;
        z-index: 3;
        height: 100%;
        transform: translate(0, -50%);
      }
      &.center {
        visibility: visible;
        z-index: 2;
        height: 90%;
        transform: translate(12.5%, -50%);
      }
      &.right {
        visibility: visible;
        z-index: -21;
        height: 80%;
        transform: translate(25%, -50%);
      }
    }
  }
}
</style>
