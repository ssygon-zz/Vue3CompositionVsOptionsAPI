<template>
  <div class="roll-the-dice">
    <h1>Total rolls: {{ count }} (Max: {{ maxRolls }})</h1>
    <button @click="roll()">Roll the dice!</button>

    <div v-if="dice != 0">
      <h2>Dice rolled: <span class="dice">{{ dice }}</span></h2>
      <p>Dice totals by:</p>
      <ul>
        <li>Reactive property: {{ diceTotal }}</li>
        <li>Computed property: {{ diceTotalComputed }}</li>
        <li>Method(): {{ diceTotalMethod() }}</li>
      </ul>
    </div>

  </div>
</template>



<script lang="ts">

/*
// 1) Options API - using data(), computed, methods
export default {
  props: {
    maxRolls: {
      type: String,
      default: ''
    }
  },
  data() {
    // Expose data for template
    // Instantiate for template
    return {
      count: 0,
      dice: 0,
      diceTotal: 0
    }
  },
  computed: {
    diceTotalComputed(): number {
      return this.diceTotal // Returning a value. Used ': number' to remove "Property 'diceTotal' does not exist on type"
    }
  },
  methods: {
    inc() {
      this.count++ // Use 'this.prop' to assign
    },
    roll() {
      if (this.count >= parseInt(this.maxRolls)) return

      this.dice = Math.floor( Math.random() * 6 ) + 1
      this.diceTotal += this.dice
      this.inc()
    },
    diceTotalMethod(): number {
      return this.diceTotal // Returning a value. Used ': number' to remove "Property 'diceTotal' does not exist on type"
    }
  }

}
*/


/*
// 2) Composition API - using ref
import { ref, computed } from "vue"

export default {
  props: {
    maxRolls: {
      type: String,
      default: ''
    }
  },
  // Initial setup
  setup(props) {

    // Instantiate for template
    let count = ref(0)
    let dice = ref(0)
    let diceTotal = ref(0)

    const inc = () => {
      count.value++ // Use a 'prop.value' to assign
    }

    const roll = () => {
      if (count.value >= parseInt(props.maxRolls)) return

      dice.value = Math.floor( Math.random() * 6 ) + 1
      diceTotal.value += dice.value
      inc()
    }

    const diceTotalMethod = () => {
      return diceTotal.value
    }

    const diceTotalComputed = computed(() => diceTotal.value)

    // Expose data for template
    return { count, dice, roll, diceTotalMethod, diceTotalComputed }
  }

}
*/






// 3) Composition API - using reactive, toRefs
import { reactive, toRefs, computed } from "vue"

export default {
  props: {
    maxRolls: {
      type: String,
      default: ''
    }
  },
  // Initial setup
  setup(props) {

    // Instantiate for template
    const state = reactive({
      count: 0,
      dice: 0,
      diceTotal: 0
    });

    const inc = () => {
      state.count++ // Use 'state.prop' to assign
    }

    const roll = () => {
      if (state.count >= parseInt(props.maxRolls)) return;

      state.dice = Math.floor( Math.random() * 6 ) + 1
      state.diceTotal += state.dice
      inc()
    }

    const diceTotalMethod = () => {
      return state.diceTotal
    }

    const diceTotalComputed = computed(() => state.diceTotal)

    // Expose data for template
    return { ...toRefs(state), roll, diceTotalMethod, diceTotalComputed }
  }

}

</script>


<style scoped>
  .roll-the-dice ul {
    width: 12rem;
    text-align: left;
    margin: auto;
    list-style-type: decimal;
  }
  .roll-the-dice .dice {
    border: 2px solid black;
    padding: 0.5rem;
  }
</style>
