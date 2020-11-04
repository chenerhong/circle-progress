<template>
  <div id="app">
    <input v-model="finishCount" @change="draw" type="number" class="input" />
    <div
      class="progress-radial"
      :style="
        point <= 50
          ? 'background-image: linear-gradient(90deg, #C40006 50%, transparent 50%, transparent), linear-gradient(' +
            deg +
            'deg, #FECC1C 50%, #C40006 50%, #C40006);'
          : 'background-image: linear-gradient(' +
            deg +
            'deg, #FECC1C 50%, transparent 50%, transparent), linear-gradient(270deg, #FECC1C 50%, #C40006 50%, #C40006)'
      "
    >
      <div class="progress-text"></div>
      <div
        class="progress-radial-end"
        :style="'transform: rotate('+(point <= 50 ? deg-90 : 270+deg)+'deg)'"
      ></div>
      <div class="progress-radial-start"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      finishCount: 1,
      totalCount: 3,
      deg: 0,
      point: 0,
    };
  },
  mounted() {
    this.draw();
  },
  methods: {
    draw() {
      let point =
        Math.floor((this.finishCount / this.totalCount) * 10000) / 100;
      let deg = 0;
      // 360度，按百分比每分3.6度
      if (point <= 50) {
        deg = Math.round(90 + point * 3.6);
      } else {
        deg = Math.round(-90 + (point - 50) * 3.6);
      }
      this.deg = deg;
      this.point = point;
    },
  },
};
</script>

<style>
.input {
  margin: 30px auto;
  display: block;
}

.progress-radial {
  position: relative;
  width: 120px;
  height: 120px;
  border-radius: 50%;
  background-image: linear-gradient(
      90deg,
      #c40006 50%,
      transparent 50%,
      transparent
    ),
    linear-gradient(90deg, #fecc1c 50%, #c40006 50%, #c40006);
  line-height: normal;
  display: flex;
  align-items: center;
  justify-content: center;
  z-index: 1;
  margin: 0 auto;
}

.progress-radial-end,
.progress-radial-start {
  width: 16px;
  height: 16px;
  top: 0;
  left: 52rpx;
  border-radius: 50%;
  background: #fecc1c;
  position: absolute;
  z-index: 999;
  line-height: normal;
  transform-origin: center 60px;
}

.progress-radial .progress-text {
  width: 88px;
  height: 88px;
  background: #ed1937;
  border-radius: 50%;
  color: #fff;
  font-size: 28px;
  text-align: center;
  line-height: 88px;
  font-weight: bold;
}
</style>
