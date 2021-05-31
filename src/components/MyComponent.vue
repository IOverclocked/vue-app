<template>
  <div>{{ quantity }}</div>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'MyComponent',
  setup() {
    const quantity = ref(12)



    return { quantity }
  }
}
</script>
