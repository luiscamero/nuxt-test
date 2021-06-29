<template>
  <div class="m-5">
    <VueSlickCarousel v-bind="settings" v-if="rivers.length">
      <div
        v-for="river in rivers"
        :key="river.id"
        class="rounded overflow-hidden shadow-lg p-5"
      >
        <img class="card-image" :src="river.image" alt="Mountain" />
        <div class="px-6 py-4">
          <div class="font-bold text-xl mb-2">
            {{ river.title }} ({{ river.length }})
          </div>
          <p class="text-gray-700 text-base river-content dark:text-white p-5">
            {{ river.description }}
          </p>
        </div>
        <div class="px-6 pt-4 pb-2">
          <p>Continent:</p>
          <span
            class="
              inline-block
              bg-gray-200
              rounded-full
              px-3
              py-1
              text-sm
              font-semibold
              text-gray-700
              mr-2
              mb-2
            "
            >{{ river.continent }}</span
          >
        </div>
        <div class="px-6 pt-4 pb-2 river-countries">
          <p>Countries:</p>
          <span
            v-for="country in river.countries"
            :key="country"
            class="
              inline-block
              bg-gray-200
              rounded-full
              px-3
              py-1
              text-sm
              font-semibold
              text-gray-700
              mr-2
              mb-2
            "
            >{{ country }}</span
          >
        </div>
      </div>
    </VueSlickCarousel>
  </div>
</template>
<style scoped>

.card-image {
  width: 100%;
  height: 30vh;
}
.river-content {
  overflow-y: auto;
  height: 20vh;
}
.river-countries {
  height: 85px;
  overflow-y: auto;
}
::-webkit-scrollbar {
  width: 5px;
}
::-webkit-scrollbar-track {
  background: #f1f1f1;
}
::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 10px;
}
::-webkit-scrollbar-thumb:hover {
  background: #555;
}
.slick-dots {
    margin-top: 1em !important;
}
</style>
<script>
import VueSlickCarousel from 'vue-slick-carousel';
import 'vue-slick-carousel/dist/vue-slick-carousel.css';
// optional style for arrows & dots
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';
export default {
  name: 'Carousel',
  components: { VueSlickCarousel },
  data() {
    return {
      rivers: [],
      settings: {
        dots: false,
        infinite: true,
        rows: 1,
        initialSlide: 0,
        speed: 500,
        slidesToShow: 3,
        slidesToScroll: 1,
        swipeToSlide: true,
        arrows: true,
        autoplay: true,
        responsive: [
          {
            breakpoint: 1200,
            settings: {
              slidesToShow: 3,
              slidesToScroll: 3,
              infinite: true,
              dots: true,
              initialSlide: 0,
            },
          },
          {
            breakpoint: 1024,
            settings: {
              slidesToShow: 2,
              slidesToScroll: 2,
              infinite: true,
              dots: true,
              initialSlide: 0,
            },
          },
          {
            breakpoint: 600,
            settings: {
              slidesToShow: 1,
              slidesToScroll: 1,
              infinite: true,
              dots: true,
              initialSlide: 0,
            },
          },
        ],
      },
    };
  },
  async fetch() {
    this.rivers = await this.$axios.$get('https://api.nuxtjs.dev/rivers');
    this.rivers.sort(
      (a, b) =>
        a.length.split(' ')[0].replace(',', '') -
        b.length.split(' ')[0].replace(',', '')
    );
  },
};
</script>
