<template>
  <Slideshow msg="Welcome to Your Vue.js + TypeScript App"/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Slideshow from './components/Slideshow.vue';

export default defineComponent({
  name: 'App',
  components: { Slideshow },
});
</script>

<style>
  /*
    To create 100% height layout on mobile devices,
    the 100% height must be applied to each child descending from html.
    vh must be avoided, it causes problems as the mobile navbar changes the window height.
  */
  html, body, #app {
    height: 100%;
  }

  body {
    margin: 0px;
    background-color: #111;
  }

  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
</style>
