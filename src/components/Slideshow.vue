<template>
  <div class='slideshow'>
    <div class='slide-container'>
      <img class='slide' :src="require('../assets/' + slides[state.currentSlideIndex])" @load="handleSlideLoad">
    </div>

    <div class='controls'>
      <!-- 'previous' button -->
      <!-- https://fontawesome.com/v5.15/icons/caret-left?style=solid -->
      <button v-if='!state.loading' class='button-previous' @click='goToPreviousSlide()'>
        <svg aria-hidden="true" focusable="false" data-prefix="fas" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 192 512">
          <path d="M192 127.338v257.324c0 17.818-21.543 26.741-34.142 14.142L29.196 270.142c-7.81-7.81-7.81-20.474 0-28.284l128.662-128.662c12.599-12.6 34.142-3.676 34.142 14.142z"></path>
        </svg>
      </button>

      <!-- 'next' button -->
      <!-- https://fontawesome.com/v5.15/icons/caret-right?style=solid -->
      <button v-if='!state.loading' class='button-next' @click='goToNextSlide()'>
        <svg aria-hidden="true" focusable="false" data-prefix="fas" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 192 512">
          <path d="M0 384.662V127.338c0-17.818 21.543-26.741 34.142-14.142l128.662 128.662c7.81 7.81 7.81 20.474 0 28.284L34.142 398.804C21.543 411.404 0 402.48 0 384.662z"></path>
        </svg>
      </button>
    </div>

    <footer>
      <span v-if='state.loading'>
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
  /*
    Do not use vh / vw units.
    Overall app height is handled in in App.vue
  */
  .slideshow {
    width: 100%;
    height: 100%;
  }

  .slide-container {
    display: flex;
    align-items: center;
    justify-content: center;

    width: 100%;
    height: 100%;
  }
  .slide {
    max-width:100%;
    max-height:100%;
  }

  .controls {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  button {
    width: 3rem;
    height: 3rem;

    display: flex;
    align-items: center;
    justify-content: center;

    background: hsla(0, 0%, 7%, 0.5);
    border: none;
    border-radius: 0.5rem;

    color: #ddd;
  }
  button.button-previous { margin-left: 1rem }
  button.button-next { margin-right: 1rem }
  button svg {
    height: 2rem;
    fill: #ddd;
  }

  /* Footer */
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
</style>
