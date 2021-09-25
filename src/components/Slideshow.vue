<template>
  <div>
    <div class='slide-container'>
      <img class='slide' :src="require('../assets/' + state.slides[state.currentSlideIndex])" @load="onImgLoad">
    </div>

    <div class='controls'>
      <div><button v-if='!state.loading' class='button-previous' @click='previous()'>&lang;</button></div>
      <div><span class='loading' v-if='state.loading'>Loading...</span></div>
      <div><button v-if='!state.loading' class='button-next' @click='next()'>&rang;</button></div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive } from 'vue'

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String
  },

  setup () {
    const state = reactive({
      slides: [
        'coffee-777612_640.jpg',
        'coins-1523383_1920.jpg',
        'posing-999199_1920.jpg',
        'raspberries-1426859_1920.jpg'
      ],
      currentSlideIndex: 0,
      loading: true,
    })

    const previous = () => {
      state.loading = true;
      state.currentSlideIndex = state.currentSlideIndex > 0 ? state.currentSlideIndex - 1 : state.slides.length - 1
    }
    const next = () => {
      state.loading = true;
      state.currentSlideIndex = state.currentSlideIndex < state.slides.length - 1 ? state.currentSlideIndex + 1 : 0
    }
    const onImgLoad = () => {
      state.loading = false
    }

    // Take keyboard input so desktop users can switch slides using the arrow keys
    const handleKeyboard = (e: KeyboardEvent) => {
      // prevent poor keyboard experience by doing nothing if we're already waiting for an image to load
      if (state.loading) return;

      switch (e.key) {
        case 'ArrowRight': next(); break
        case 'ArrowUp': next(); break

        case 'ArrowLeft': previous(); break
        case 'ArrowDown': previous(); break
      }
    }
    document.addEventListener('keyup', handleKeyboard)

    return { state, previous, next, onImgLoad }
  }
})
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
    outline: 1px dotted cyan;
  }

  button {
    width: 3rem;
    height: 4rem;

    display: flex;
    align-items: center;
    justify-content: center;

    background: hsla(0, 0%, 0%, 0.25);
    border: none;
    border-radius: 0.5rem;

    font-size: 3rem;
    color: #ddd;
  }

  .button-previous { margin-left: 1rem }
  .button-next { margin-right: 1rem }

  .loading {
    background: hsla(0, 0%, 0%, 0.25);
    border-radius: 0.5rem;
    color: #ddd;
    font-size: 1rem;
    padding-left: 0.5rem;
    padding-right: 0.5rem;
  }
</style>
