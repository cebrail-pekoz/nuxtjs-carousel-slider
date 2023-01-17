<template>
  <div>
    <div class="carousel-indicators">
      <button class="carousel-indicators-item" v-for="(item, index) in total" :key="index"
        :class="{ active: currentIndex === index }" @click="$emit('switch', index)">
      </button>
    </div>
  </div>
</template>

<script>
export default {
  emits: ['switch'],
  props: ["total", "currentIndex"]
}
</script>

<style scoped>

.carousel-indicators{
  position: absolute;
  transform: translateX(-50%);
  left: 50%;
  /* background-color: #999; */
  bottom: 1.5em;
  z-index: 2;
}

.carousel-indicators-item{
  width: 15px;
  height: 15px;
  border: none;
  background-color: red;
  margin: 0.2em;
  opacity: .5;
  border-radius: 50%;
  cursor: pointer;
}

.active{
  opacity: 1;
}

</style>