<template>
  <div>
    <Navbar :show-carousel="showCarousel" v-on:goBack="goBack()" />
    <div class="welcome" v-if="!showCarousel">
      <h3 class="font-bold text-center">Welcome!</h3>
      <div class="width-full text-center mt-5">
        <button
          class="
            bg-blue-500
            hover:bg-blue-700
            text-white
            font-bold
            py-2
            px-4
            rounded
          "
          @click="showCarousel = !showCarousel"
        >
          Discover the rivers
        </button>
      </div>
    </div>
    <div class="carousel px-5" v-if="showCarousel">
      <Carousel />
    </div>
  </div>
</template>
<script>
import Carousel from '../components/Carousel';
import Navbar from '../components/Navbar';
export default {
  name: 'index',
  components: { Carousel, Navbar },
  data() {
    return {
      showCarousel: false,
    };
  },
  methods: {
    goBack() {
      this.showCarousel = !this.showCarousel;
    },
  },
};
</script>
