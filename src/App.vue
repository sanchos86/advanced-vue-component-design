<template>
  <div id="app">
    <ToggleInput v-model="checked" />
    <hr>
  </div>
</template>

<script>
import ToggleInput from './components/ToggleInput.vue'

export default {
  name: 'App',
  components: {
    ToggleInput
  },
  data() {
    return {
      checked: false
    };
  }
}
</script>

<style>
:root {
  --color-primary: #007bff;
  --color-secondary: #dae0e5;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
