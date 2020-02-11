<template>
  <div id="app">
    <Todolist />
  </div>
</template>

<script>
import Todolist from './components/Todolist.vue';

export default {
  name: 'App',
  components: {
    Todolist,
  },
};
</script>

<style>
#app {
  font-family: Laila, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  background: linear-gradient(to bottom, #984CFF, #00D5FA);
	font-family: Laila;
}
</style>
