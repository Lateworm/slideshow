<template>
  <div>
    <div class='slide-container'>
      <img class='slide' :src="require('../assets/' + slides[state.currentSlideIndex])" @load="handleSlideLoad">
    </div>

    <div class='controls'>
      <div><button v-if='!state.loading' class='button-previous' @click='goToPreviousSlide()'>&lang;</button></div>
      <div><button v-if='!state.loading' class='button-next' @click='goToNextSlide()'>&rang;</button></div>
    </div>

    <footer>
      <span class='loading' v-if='state.loading'>
        Loading...
      </span>
      <span v-if='!state.loading'>
        {{ slides[state.currentSlideIndex] }} - viewed {{ state.slideViewCounts[state.currentSlideIndex] }} times(s) this session
      </span>
    </footer>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String,
  },

  setup () {
    // data and state
    const slides = [
      'coffee-777612_640.jpg',
      'coins-1523383_1920.jpg',
      'posing-999199_1920.jpg',
      'raspberries-1426859_1920.jpg',
    ];
    const state = reactive({
      currentSlideIndex: 0,
      slideViewCounts: [0, 0, 0, 0],
      loading: true,
    });

    // navigation
    const goToPreviousSlide = () => {
      state.loading = true;
      state.currentSlideIndex = state.currentSlideIndex > 0 ? state.currentSlideIndex - 1 : slides.length - 1;
    };
    const goToNextSlide = () => {
      state.loading = true;
      state.currentSlideIndex = state.currentSlideIndex < slides.length - 1 ? state.currentSlideIndex + 1 : 0;
    };
    const handleSlideLoad = () => {
      state.loading = false;
      state.slideViewCounts[state.currentSlideIndex]++;
    };

    // keyboard interface
    const handleKeyboard = (e: KeyboardEvent) => {
      if (state.loading) return;

      switch (e.key) {
        case 'ArrowRight': goToNextSlide(); break;
        case 'ArrowUp': goToNextSlide(); break;

        case 'ArrowLeft': goToPreviousSlide(); break;
        case 'ArrowDown': goToPreviousSlide(); break;
      }
    };
    document.addEventListener('keyup', handleKeyboard);

    return {
      slides,
      state,
      goToPreviousSlide,
      goToNextSlide,
      handleSlideLoad,
    };
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .slide-container {
    display: flex;
    align-items: center;
    justify-content: center;

    width: 100vw;
    height: 100vh;
  }
  .slide {
    max-width:100%;
    max-height:100%;
  }

  .controls {
    position: absolute;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  button {
    width: 3rem;
    height: 4rem;

    display: flex;
    align-items: center;
    justify-content: center;

    background: hsla(0, 0%, 7%, 0.5);
    border: none;
    border-radius: 0.5rem;

    font-size: 3rem;
    color: #ddd;
  }
  button.button-previous { margin-left: 1rem }
  button.button-next { margin-right: 1rem }

  footer {
    position: absolute;
    bottom: 0;
    left: 0;
    margin: 1rem;
    background: hsla(0, 0%, 7%, 0.5);
    color: #ddd;
    border-radius: 0.5rem;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }

  .loading {
    background: hsla(0, 0%, 7%, 0.5);
    border-radius: 0.5rem;
    color: #ddd;
    font-size: 1rem;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
</style>
