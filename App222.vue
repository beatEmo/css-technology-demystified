<template>
  <div class="app">
    <div class="container">
      <div class="cude" ref="cude">
        <div
          v-for="(item, index) of data"
          :key="index"
          :style="{ backgroundColor: item.color, '--width': itemWidth }"
          class="box"
        >
          {{ item.content }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      itemWidth: 0,
      data: [
        { content: "swiper 1", color: "pink" },
        { content: "swiper 2", color: "red" },
        { content: "swiper 3", color: "skyblue" }
      ]
    };
  },
  mounted() {
    this.itemWidth = this.$refs.cude.offsetWidth;
    console.log(this.$refs.cude.offsetWidth);
  },
  methods: {}
};
</script>
<style>
html,
body {
  margin: 0 !important;
  padding: 0 !important;
}
</style>
<style lang="scss" scoped>
@function pi() {
  @return 3.14159265359;
}
@function rad($angle) {
  $unit: unit($angle);
  $unitless: $angle / ($angle * 0 + 1);
  // If the angle has 'deg' as unit, convert to radians.
  @if $unit == deg {
    $unitless: $unitless / 180 * pi();
  }
  @return $unitless;
}
@function sin($angle) {
  $sin: 0;
  $angle: rad($angle);
  // Iterate a bunch of times.
  @for $i from 0 through 10 {
    $sin: $sin + pow(-1, $i) * pow($angle, (2 * $i + 1)) / fact(2 * $i + 1);
  }
  @return $sin;
}
@function cos($angle) {
  $cos: 0;
  $angle: rad($angle);
  // Iterate a bunch of times.
  @for $i from 0 through 10 {
    $cos: $cos + pow(-1, $i) * pow($angle, 2 * $i) / fact(2 * $i);
  }
  @return $cos;
}

@function tan($angle) {
  @return sin($angle) / cos($angle);
}
.app {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  .container {
    width: calc(100% - 20px);
    height: 200px;
    perspective: 800px;
    border: 1px solid black;
    .cude {
      position: relative;
      width: 100%;
      height: 100%;
      transform-style: preserve-3d;
      transform-origin: 50% 50% -54.8px;
      /* transform: rotateX(120deg); */
      .box {
        width: 100%;
        height: inherit;
        position: absolute;
        /* position: absolute; */
        &:nth-child(1) {
          transform: rotateX(0deg);
        }
        &:nth-child(2) {
          transform-origin: center center
            calc(-(var(--width) / 2) * tan(30 * pi / 180) px);
          transform: rotateX(120deg);
        }
        &:nth-child(3) {
          /* transform-origin: 0 100% 0px; */
          transform: rotateX(240deg);
        }
      }
    }
  }
}
</style>
