<template>
  <div id="app">
    <ToggleInput v-model="checked" />
    <hr>
    <DatePicker v-model="date" :options="{ firstDay: 1 }" />
    <hr>
    <AnnouncementModal />
    <hr>
  </div>
</template>

<script>
import ToggleInput from './components/ToggleInput.vue'
import DatePicker from '@/components/DatePicker';
import AnnouncementModal from '@/components/AnnouncementModal';

export default {
  name: 'App',
  components: {
    DatePicker,
    ToggleInput,
    AnnouncementModal
  },
  data() {
    return {
      checked: false,
      date: new Date()
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
