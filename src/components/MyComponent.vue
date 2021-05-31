<template>
  <h2>{{ title }}</h2>
  <div>{{ quantity }}</div>
  <div>{{ tax }}</div>
  <button @click="add" >Add</button>
</template>

<script>
import { computed, reactive, ref, toRefs, watch } from 'vue'

export default {
  name: 'MyComponent',
  setup() {
    const title = ref('MyComponent')

    const state = reactive({
      quantity: 0,
      price: 100,
      totalPrice: computed(() => state.price * state.quantity),
      tax: computed(() => state.quantity * 0.23)
    })

    function add() {
      state.quantity++
    }

    watch(() => state.quantity, (prevQuantity, quantity) => {
      console.log(prevQuantity, quantity)
    })

    return { title, add, ...toRefs(state) }
  }
}
</script>
