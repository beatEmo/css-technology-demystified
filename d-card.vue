<template>
  <div class="dcard-container">
    <div class="cube">
      <div class="top"></div>
      <div>
        <span style="--i: 0">1</span>
        <span style="--i: 1">2</span>
        <span style="--i: 2">3</span>
        <span style="--i: 3">4</span>
      </div>
    </div>
    <div style="margin-top: -700px">
      <button @click="aaa">dadasd</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "dCard",
  data() {
    return {
      a: 1
    };
  },
  methods: {
    aaa() {
      console.log(this.a);
      document.querySelector(
        ".cube"
      ).style.transform = `rotateX(-30deg) rotateY(${(this.a % 4) * 90}deg)`;
      this.a++;
      // if (this.a === 5) {
      //   this.a = 1;
      // }
    }
  }
};
</script>

<style lang="scss" scoped>
//CSS
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.dcardcontainer {
  display: flex;
  justify-content: center;
  align-content: center;
}
body {
  display: flex;
  min-height: 100vh;
  overflow: hidden;
  justify-content: center;
  align-items: center;
  background: #050505;
}

.cube {
  display: flex;
  justify-content: center;
  align-content: center;
  position: relative;
  left: 200px;
  width: 300px;
  height: 300px;
  transform-style: preserve-3d;
  transition: all 3s;
  /* animation: animate 4s linear infinite; */
  transform: rotateX(-30deg);
}

@keyframes animate {
  0% {
    transform: rotateX(-30deg) rotateY(0deg);
  }
  100% {
    transform: rotateX(-30deg) rotateY(360deg);
  }
}

.cube div {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  transform-style: preserve-3d;
}

.cube div span {
  color: red;
  font-size: 24px;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(#151515, #00ec00);
  transform: rotateY(calc(90deg * var(--i))) translateZ(150px);
}

.top {
  position: absolute;
  top: 0;
  left: 0;
  width: 300px;
  height: 300px;
  background: #222;
  transform: rotateX(90deg) translateZ(150px);
}

.top::before {
  content: "";
  position: absolute;
  top: 0;
  left: 0;
  width: 300px;
  height: 300px;
  background: #0f0;
  transform: translateZ(-380px);
  filter: blur(20px);
  box-shadow: 0 0 120px rgba(0, 255, 0, 0.2), 0 0 200px rgba(0, 255, 0, 0.4),
    0 0 300px rgba(0, 255, 0, 0.6), 0 0 400px rgba(0, 255, 0, 0.8),
    0 0 500px rgba(0, 255, 0, 1);
}
</style>
