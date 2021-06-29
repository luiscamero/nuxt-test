<template>
  <div class="flex justify-between items-center mx-5 mt-5">
    <div>
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
        @click="$emit('goBack')"
        v-if="showCarousel"
      >
        Go back
      </button>
    </div>
    <ul>
      <li v-for="color of colors" :key="color">
        <component :is="`icon-${color}`" @click="setColor(color)" />
      </li>
    </ul>
  </div>
</template>
<style scoped>
ul {
  width: fit-content;
  list-style: none;
  padding: 0;
  margin: 0;
  margin-right: 1em;
  display: flex;
  align-items: center;
  flex-direction: row;
}
ul li {
  display: inline-block;
  padding: 5px;
}
p {
  margin: 0;
  padding-top: 5px;
  padding-bottom: 20px;
}
</style>
<script>
import IconLight from '@/assets/icons/light.svg?inline';
import IconDark from '@/assets/icons/dark.svg?inline';
export default {
  name: 'navbar',
  components: {
    IconLight,
    IconDark,
  },
  data() {
    return {
      colors: ['light', 'dark'],
    };
  },
  props: ['showCarousel'],
  methods: {
    setColor(color) {
      $nuxt.$colorMode.preference = color;
      const html = document.getElementsByTagName('html')[0];
      if (color === 'dark') {
        html.classList.add('dark');
      } else {
        html.classList.remove('dark');
      }
    },
  },
  mounted() {
    const html = document.getElementsByTagName('html')[0];
    if (html.classList.contains('dark-mode')) {
      html.classList.add('dark');
    }
  },
};
</script>
