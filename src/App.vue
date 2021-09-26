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
