<template>
  <div id="app">
    <RollTheDice maxRolls="10"/>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import RollTheDice from './components/RollTheDice.vue';

@Options({
  components: {
    RollTheDice
  },
})
export default class App extends Vue {}
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
