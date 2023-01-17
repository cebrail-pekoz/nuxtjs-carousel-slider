<template>
  <div>
    <transition :name="transitionEffect">
      <div class="carousel-item" v-if="currentSlide === index" @mouseenter="$emit('mouseenter')"
        @mouseout="$emit('mouseout')">
        <img :src="slide" :alt="slide.split('/').pop().split('.').shift()"
          :title="slide.split('/').pop().split('.').shift()" />

      </div>
    </transition>
  </div>
</template>


<script>
export default {
  emits: ['mouseenter', 'mouseout'],
  props: ['slide', "currentSlide", "index", "direction", "myWidth"],

  computed: {
    transitionEffect() {
      return this.direction === "right" ? "slide-out" : "slide-in"
    }
  }

}
</script>

<style scoped>

.carousel-item{
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.images{
  display: flex;
  justify-content: center;
  align-items: center;
}

.slide-in-enter-active, .slide-in-leave-active,
.slide-out-enter-active, .slide-out-leave-active{
  transition: all 1s ease;
}

.slide-in-enter{
  transform: translateX(-100%);
}

.slide-in-leave-to{
  transform: translateX(100%);
}

.slide-out-enter{
  transform: translateX(100%);
}

.slide-out-leave-to{
  transform: translateX(-100%);
}

img{
  object-fit: cover;
  width: 100%;
}

</style>