<template>
  <div>
    <div class="carousel">
      <div class="carousel-inner">
        <app-indicators v-if="indicators" :total="slides.length" :current-index="currentSlide"
          @switch="switchSlide($event)">
        </app-indicators>

        <app-item class="deneme" v-for="(slide, index) in slides" :key="`item-${index}`" :slide="slide"
          :current-slide="currentSlide" :index="index" :direction="direction" @mouseenter="stopSliderTimer"
          @mouseout="startSliderTimer" :myWidth="myWidth">
        </app-item>

        <app-controls v-if="controls" @prev="prev" @next="next">
        </app-controls>
      </div>
    </div>
  </div>
</template>


<script>

import Item from './Item.vue';
import Control from './Control.vue';
import Indicators from './Indicators.vue';


export default {
  props: {
    slides: {
      type: Array,
      required: true
    },
    controls: {
      type: Boolean,
      default: false
    },
    indicators: {
      type: Boolean,
      default: false
    },
    interval: {
      type: Number,
      default: 3000
    },
    myWidth: {
      type: Number,
      default: 100
    }
  },
  components: {
    appItem: Item,
    appControls: Control,
    appIndicators: Indicators
  },
  data() {
    return {
      currentSlide: 0,
      slideInterval: null,
      direction: "right"
    }
  },
  methods: {
    setCurrentSlide(index) {
      this.currentSlide = index;
    },
    prev(step = -1) {
      const index = this.currentSlide > 0 ? this.currentSlide + step : this.slides.length - 1;
      this.setCurrentSlide(index);
      this.direction = "left"
      this.startSliderTimer()
    },
    _next(step = 1) {
      const index = this.currentSlide < this.slides.length - 1 ? this.currentSlide + step : 0;
      this.setCurrentSlide(index);
      this.direction = "right"
    },
    next(step = 1) {
      this._next(step)
      this.startSliderTimer()
    },
    startSliderTimer() {
      this.stopSliderTimer();
      this.slideInterval = setInterval(() => {
        this._next();
      }, this.interval)
    },
    stopSliderTimer() {
      clearInterval(this.slideInterval);
    },
    switchSlide(index) {
      const step = index - this.currentSlide;
      if (step > 0) {
        this.next(step)
      } else {
        this.prev(step)
      }
    }
  },
  mounted() {
    this.startSliderTimer();
  },
  beforeMount() {
    this.stopSliderTimer();
  }

}
</script>

<style scoped>

.carousel{
  display: flex;
  justify-content: center;
}

.carousel-inner{
  position: relative;
  width: 900px;
  height: 400px;
  overflow: hidden;
  border: 1px solid red;
}

</style>