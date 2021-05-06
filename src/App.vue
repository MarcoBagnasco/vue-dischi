<template>
  <div id="app">
    <!-- Header -->
    <Header />

    <!-- Main -->
    <Main />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Main from '@/components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main,
  }
}
</script>

<style lang="scss">
@import "~@fontsource/lato/index.css";
@import "~@fontsource/lato/700.css";

  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Lato', sans-serif;
  }
  body {
    color: #fff;
    background-color: #1d2d3c;
  }
  img{
    max-width: 100%;
  }
</style>
