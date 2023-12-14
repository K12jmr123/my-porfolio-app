<!-- App.vue -->
<template>
  <div id="app">
    <h1>Set Alarm Clock</h1>
    <AlarmClock />
  </div>
</template>

<script>
import AlarmClock from './components/AlarmClock.vue';

export default {
  name: 'App',
  components: {
    AlarmClock,
  },
};
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-size: 2em;
  margin-bottom: 20px;
}
</style>
