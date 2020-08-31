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

<style lang="scss">
@import "styles/app.scss";
</style>
