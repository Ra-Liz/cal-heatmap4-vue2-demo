<template>
  <div id="app">
    <CalendarTest />
  </div>
</template>

<script>
import CalendarTest from "./components/CalendarTest.vue";

export default {
  name: "App",
  components: {
    CalendarTest,
  },
};
</script>

<style>
#app {
  background-color: #2c3e503f;
  color: #2c3e50;
  height: 100%;
  width: 100%;
  padding: 0;
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
