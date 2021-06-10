<template>
  <h2>{{ title }}</h2>
  <div>{{ quantity }}</div>
  <div>{{ tax }}</div>
  <button 
    class="btn" 
    @click="add" 
    :disabled="quantity >= 10"
    :class="quantity > 0 && 'btn--warning'"
  >
    Add
  </button>
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

    const styles = reactive({
      btn: {
        backgroundColor: '#17a2b8',
        color: '#fff'
      }
    })

    return { title, add, ...toRefs(state), ...toRefs(styles) }
  }
}
</script>

<style lang="scss">
  .btn {
    color: #fff;
    background-color: #369b6d;
    border: none;
    padding: 5px 10px;
    font-size: 16px;
    cursor: pointer;
    transition: background-color 150ms ease-in;

    &--warning {
      background-color: #ffc107;
      color: #000;
    }

    &:disabled {
      cursor: default;
      background-color: #4f4f4f;
      opacity: 0.8;
    }
  }
</style>
