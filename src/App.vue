<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <Jokes/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import Jokes from './components/jokes.vue';

export default {
  name: 'app',
  components: {
    HelloWorld,
    Jokes,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
