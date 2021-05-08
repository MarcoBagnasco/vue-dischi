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
// FONT
@import "~@fontsource/lato/index.css";
@import "~@fontsource/lato/700.css";

// GENERAL
@import '@/styles/general.scss';

// UTILITIES
@import '@/styles/utilities.scss';
</style>