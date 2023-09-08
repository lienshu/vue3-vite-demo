<script setup lang="ts">
import { ref } from 'vue'
import VueJsx from './VueJsx.vue'
// import VueCommon from './VueCommon.vue'
import ScrollIntoView from './ScrollIntoView.vue'

defineProps<{ msg?: string }>()

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>
  <VueJsx :msg="msg"/>
  <!-- <VueCommon /> -->
  <ScrollIntoView />
  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
