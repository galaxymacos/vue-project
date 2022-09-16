<script setup>
import { ref, reactive } from 'vue'
const count = ref(0)  // ref can be used to create a reactive variable (both object and primitive)
const state = reactive({  // reactive only works on objects
  count: 0
})
const increment = () => {
  state.count++
}
</script>

<template>
  <button @click="increment">Increment count</button>
  {{ state.count }}
</template>