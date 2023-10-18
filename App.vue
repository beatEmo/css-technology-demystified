<template>
  <div class="native-container">
    <div
      class="cube"
      style="
         {
          '--width':355 ;
        }
      "
    >
      <span>1</span>
      <span>2</span>
      <span>3</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "spriteCube",
  data() {
    return {};<template>
  <div class="native-container">
    <div
      class="cube"
      style="
         {
          '--width':355 ;
        }
      "
    >
      <span>1</span>
      <span>2</span>
      <span>3</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "spriteCube",
  data() {
    return {
      boxHeight: 0,
      angle: 0
    };
  },
  mounted() {
    this.boxHeight = document.querySelector(".cube").offsetHeight;

    var stlyleNode = document.createElement("style");
    //外角
    // var degOut = 120;
    //内角
    var degIn = 60;
    var cssText = "";

    var mianNode = document.querySelector(".native-container > .cube > span");
    //棱长
    var length = mianNode.offsetHeight;
    cssText +=
      ".native-container > .cube{transform-origin: center center -" +
      (length / 2) * Math.tan(((degIn / 2) * Math.PI) / 180) +
      "px;}";
    cssText +=
      ".native-container > .cube > span{transform-origin: center center -" +
      (length / 2) * Math.tan(((degIn / 2) * Math.PI) / 180) +
      "px;}";
    stlyleNode.innerHTML = cssText;
    document.head.appendChild(stlyleNode);

    let box = document.querySelector("body"); // 监听对象
    let startTime = ""; // 触摸开始时间
    let startDistanceX = ""; // 触摸开始X轴位置
    let startDistanceY = ""; // 触摸开始Y轴位置
    let endTime = ""; // 触摸结束时间
    let endDistanceX = ""; // 触摸结束X轴位置
    let endDistanceY = ""; // 触摸结束Y轴位置
    let moveTime = ""; // 触摸时间
    let moveDistanceX = ""; // 触摸移动X轴距离
    let moveDistanceY = ""; // 触摸移动Y轴距离
    box.addEventListener("touchstart", (e) => {
      startTime = new Date().getTime();
      startDistanceX = e.touches[0].screenX;
      startDistanceY = e.touches[0].screenY;
    });
    box.addEventListener("touchend", (e) => {
      endTime = new Date().getTime();
      endDistanceX = e.changedTouches[0].screenX;
      endDistanceY = e.changedTouches[0].screenY;
      moveTime = endTime - startTime;
      moveDistanceX = startDistanceX - endDistanceX;
      moveDistanceY = startDistanceY - endDistanceY;
      // 判断滑动距离超过40 且 时间小于500毫秒
      if (
        (Math.abs(moveDistanceX) > 40 || Math.abs(moveDistanceY) > 40) &&
        moveTime < 500
      ) {
        // 判断X轴移动的距离是否大于Y轴移动的距离
        if (Math.abs(moveDistanceX) > Math.abs(moveDistanceY)) {
          // 左右
          console.log(moveDistanceX > 0 ? "左" : "右");
        } else {
          // 上下
          console.log(moveDistanceY > 0 ? "上" : "下");
          const a = Math.round(Math.abs(moveDistanceY) / (this.boxHeight / 2));
          console.log(a);
          if (moveDistanceY > 0) {
            this.angle += (a % 3) * 120;
          } else {
            this.angle -= (a % 3) * 120;
          }
          document.querySelector(
            ".cube"
          ).style.transform = `rotateX(${this.angle}deg)`;
          console.log(this.angle, "============");
          // document.querySelector(".cube").style.transform = `rotateX(${
          //   moveDistanceY > 0 ? "" : "-"
          // }${a * 120}deg)`;
        }
      }
    });
  },
  methods: {
    getDirection(startx, starty, endx, endy) {
      var angx = endx - startx;
      var angy = endy - starty;
      var result = 0;
      //如果滑动距离太短
      if (Math.abs(angx) < 2 && Math.abs(angy) < 2) {
        return result;
      }
      var angle = this.getAngle(angx, angy);
      if (angle >= -135 && angle <= -45) {
        result = 1;
      } else if (angle > 45 && angle < 135) {
        result = 2;
      }
      // else if (
      //   (angle >= 135 && angle <= 180) ||
      //   (angle >= -180 && angle < -135)
      // ) {
      //   result = 3;
      // } else if (angle >= -45 && angle <= 45) {
      //   result = 4;
      // }
      return [result, angy];
    },
    getAngle(angx, angy) {
      return (Math.atan2(angy, angx) * 180) / Math.PI;
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
.native-container {
  width: 100vw;
  height: 2000px;
  overflow-y: auto;
  perspective: 800px;
  display: flex;
  justify-content: center;
  /* position: absolute; */
  /* left: 0;
  top: 0;
  right: 0;
  bottom: 0; */
  /* margin: auto; */
  border: 1px solid #000;
  perspective: 1000px;
  .cube {
    /* position: relative; */
    width: calc(100% - 20px);
    height: 216px;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    transition: 1s transform;
    transform-style: preserve-3d;
    /* padding: 20px; */
    & > span {
      position: absolute;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;
      text-align: center;
      font: 50px/300px "微软雅黑";
      /*transform-origin: center center -28.867513459481287px;*/
      backface-visibility: hidden;
      /* transform-origin: center center -0.98px; */
      &:nth-child(1) {
        background: red;
        transform: rotateX(0deg);
        /* transform: rotateX(0deg); */
      }
      &:nth-child(2) {
        background: skyblue;
        transform: rotateX(120deg);
        /* transform: rotateX(120deg); */
      }
      &:nth-child(3) {
        background: pink;
        transform: rotateX(240deg);
        /* transform: rotateX(240deg); */
      }
    }
  }
}
</style>

  },
  mounted() {
    var stlyleNode = document.createElement("style");
    //外角
    var degOut = 120;
    //内角
    var degIn = 60;
    var cssText = "";
    for (var i = 0; i < 3; i++) {
      cssText +=
        ".native-container > .cube > span:nth-child(" +
        (i + 1) +
        "){transform: rotateX(" +
        i * degOut +
        "deg);}";
    }
    var mianNode = document.querySelector(".native-container > .cube > span");
    //棱长
    var length = mianNode.offsetHeight;
    cssText +=
      ".native-container > .cube{transform-origin: center center -" +
      (length / 2) * Math.tan(((degIn / 2) * Math.PI) / 180) +
      "px;}";
    cssText +=
      ".native-container > .cube > span{transform-origin: center center -" +
      (length / 2) * Math.tan(((degIn / 2) * Math.PI) / 180) +
      "px;}";
    stlyleNode.innerHTML = cssText;
    document.head.appendChild(stlyleNode);

    let box = document.querySelector("body"); // 监听对象
    let startTime = ""; // 触摸开始时间
    let startDistanceX = ""; // 触摸开始X轴位置
    let startDistanceY = ""; // 触摸开始Y轴位置
    let endTime = ""; // 触摸结束时间
    let endDistanceX = ""; // 触摸结束X轴位置
    let endDistanceY = ""; // 触摸结束Y轴位置
    let moveTime = ""; // 触摸时间
    let moveDistanceX = ""; // 触摸移动X轴距离
    let moveDistanceY = ""; // 触摸移动Y轴距离
    box.addEventListener("touchstart", (e) => {
      startTime = new Date().getTime();
      startDistanceX = e.touches[0].screenX;
      startDistanceY = e.touches[0].screenY;
    });
    box.addEventListener("touchend", (e) => {
      endTime = new Date().getTime();
      endDistanceX = e.changedTouches[0].screenX;
      endDistanceY = e.changedTouches[0].screenY;
      moveTime = endTime - startTime;
      moveDistanceX = startDistanceX - endDistanceX;
      moveDistanceY = startDistanceY - endDistanceY;
      console.log(moveDistanceX, moveDistanceY);
      // 判断滑动距离超过40 且 时间小于500毫秒
      if (
        (Math.abs(moveDistanceX) > 40 || Math.abs(moveDistanceY) > 40) &&
        moveTime < 500
      ) {
        // 判断X轴移动的距离是否大于Y轴移动的距离
        if (Math.abs(moveDistanceX) > Math.abs(moveDistanceY)) {
          // 左右
          console.log(moveDistanceX > 0 ? "左" : "右");
        } else {
          // 上下
          console.log(moveDistanceY > 0 ? "上" : "下");
          const a = Math.round(
            Math.abs(moveDistanceY) /
              document.querySelector(".cube").offsetHeight
          );
          document.querySelector(".cube").style.transform = `rotateX(${
            moveDistanceY > 0 ? "" : "-"
          }${a * 120}deg)`;
          console.log(
            a,
            moveDistanceY,
            document.querySelector(".cube").offsetHeight,
            "---------"
          );
        }
      }
    });
  },
  methods: {
    getDirection(startx, starty, endx, endy) {
      var angx = endx - startx;
      var angy = endy - starty;
      var result = 0;
      //如果滑动距离太短
      if (Math.abs(angx) < 2 && Math.abs(angy) < 2) {
        return result;
      }
      var angle = this.getAngle(angx, angy);
      if (angle >= -135 && angle <= -45) {
        result = 1;
      } else if (angle > 45 && angle < 135) {
        result = 2;
      }
      // else if (
      //   (angle >= 135 && angle <= 180) ||
      //   (angle >= -180 && angle < -135)
      // ) {
      //   result = 3;
      // } else if (angle >= -45 && angle <= 45) {
      //   result = 4;
      // }
      return [result, angy];
    },
    getAngle(angx, angy) {
      return (Math.atan2(angy, angx) * 180) / Math.PI;
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
.native-container {
  width: 100vw;
  height: 2000px;
  overflow-y: auto;
  perspective: 800px;
  display: flex;
  justify-content: center;
  /* position: absolute; */
  /* left: 0;
  top: 0;
  right: 0;
  bottom: 0; */
  /* margin: auto; */
  border: 1px solid #000;
  perspective: 1000px;
  .cube {
    /* position: relative; */
    width: calc(100% - 20px);
    height: 216px;
    position: absolute;
    left: 0;
    top: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    transition: 1s transform;
    transform-style: preserve-3d;
    /* padding: 20px; */
    & > span {
      position: absolute;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 100%;
      height: 100%;
      text-align: center;
      font: 50px/300px "微软雅黑";
      /*transform-origin: center center -28.867513459481287px;*/
      backface-visibility: hidden;
      /* transform-origin: center center -0.98px; */
      &:nth-child(1) {
        background: red;
        /* transform: rotateX(0deg); */
      }
      &:nth-child(2) {
        background: skyblue;
        /* transform: rotateX(120deg); */
      }
      &:nth-child(3) {
        background: pink;
        /* transform: rotateX(240deg); */
      }
    }
  }
}
</style>
