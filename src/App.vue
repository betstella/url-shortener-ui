<template>
  <div id="app">
    <ShortenUrlForm />
  </div>
</template>

<script>
import ShortenUrlForm from './components/ShortenUrlForm.vue';

export default {
  components: {
    ShortenUrlForm
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
