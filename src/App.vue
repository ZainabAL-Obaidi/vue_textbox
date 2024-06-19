<template>
  <div id="app">
    <TextBox />
  </div>
</template>

<script>
import TextBox from './components/TextBox.vue';

export default {
  name: 'App',
  components: {
    TextBox
  }
};
</script>

<style>
#app {
  font-family: Arial, Helvetica, sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
