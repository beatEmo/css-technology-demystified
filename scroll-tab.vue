<template>
  <div class="scroll-container">
    <div class="container">
      <ul id="scale-carousel-map">
        <li
          v-for="(item, index) of data"
          :key="index"
          class="slide"
          :style="{ 'background-color': item.color }"
          :class="{
            current: index === current,
            [`${'current-show'}`]: index === currentShow,
            [`${'middle-show'}`]: index === middleShow,
            [`${'last-show'}`]: index === lastShow
          }"
        >
          {{ item.content }}
        </li>
      </ul>
    </div>
    <div>
      <button id="zuo" @click="handlezuo">zuo</button>
      <button id="you">you</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "scrollTab",
  data() {
    return {
      data: [
        {
          color: "#ee3f4d",
          content: "Slide 1"
        },
        {
          color: "#2376b7",
          content: "Slide 2"
        },
        {
          color: "#fc8c23",
          content: "Slide 3"
        },
        {
          color: "skyblue",
          content: "Slide 4"
        },
        {
          color: "pink",
          content: "Slide 5"
        }
      ],
      current: null,
      currentShow: 0,
      middleShow: 1,
      lastShow: 2
    };
  },
  methods: {
    handlezuo() {
      console.log(this.current);
      if (this.current >= this.data.length - 1) {
        this.current = null;
      }
      // eslint-disable-next-line valid-typeof
      if (typeof this.current !== "number") {
        this.current = 0;
      } else {
        this.current++;
      }
      this.currentShow = (this.current + 1) % this.data.length;
      this.middleShow = (this.current + 2) % this.data.length;
      this.lastShow = (this.current + 3) % this.data.length;
      console.log(this.current, "------------");
    }
  }
};
</script>

<style lang="scss" scoped>
.container {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: space-around;
}
/* --------  Scale Carousel Map  -------- */
#scale-carousel-map {
  position: relative;
  display: flex;
  overflow: hidden;
  width: calc(100% - 20px);
  height: 192px;
}
#scale-carousel-map .slide {
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
  /* width: inherit; */
  /* width: calc(100% - 20px); */
  width: 300px;
  height: 100%;
  border-radius: 4px;
  color: #fff;
  font-size: 1.5rem;
  transition: all linear 0.8s;
  z-index: 0;
  display: none;
}
.current {
  transform: translate(-100%);
  z-index: 12 !important;
  display: flex !important;
}
.current-show {
  transform: translateX(0);
  z-index: 4 !important;
  display: flex !important;
}
.middle-show {
  transform: translateX(10%);
  z-index: 2 !important;
  display: flex !important;
}
.last-show {
  transform: translateX(20%);
  z-index: 1 !important;
  display: flex !important;
}
</style>
