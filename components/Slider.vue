<template>
  <div>
    <!-- <app-testcarousel :slides="images" :interval="4000" controls indicators></app-testcarousel> -->
    <app-carousel :slides="slides" :interval="40000" controls indicators :myWidth="myWidth"></app-carousel>
    <h2>img</h2>
    <div class="slide container" v-for="(slide, index) in slides" :key="index">
      <img :src="`${slide}`" :alt="slide.split('/').pop().split('.').shift()"
        :title="slide.split('/').pop().split('.').shift()" width="100%" height="auto"
        sizes="(max-width: 1140px) 1140px, (max-width: 768px) 768px, (max-width: 320px) 320px" />
    </div>
  </div>
</template>


<script>
import Carousel from './Carousel.vue';
export default {
  components: {
    appCarousel: Carousel
  },
  data() {
    return {
      myWidth: 50
    }
  },
  created() {
    this.slides;
  },
  computed: {
    slides() {
      const pathImage = require.context('../static/slider/', false, /\.*$/);
      let imagesPath = (pathImage.keys().map(pathImage));
      return imagesPath;
    }
  }

}
</script>

<style lang="scss" scoped>
.p {
  .span {
    background-color: red;
    color: $white;
  }
}
</style>