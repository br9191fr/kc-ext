<template>
  <div v-if="isInitialized">
    <button @click="inc()">Clicked is really new now {{ countState.count }} times.</button>
  </div>
</template>
// script now
<script>
import {clickStore} from "../store/click-store";
import {onBeforeMount} from 'vue'
let myData = {'info': 12,"other": "any"}
export default {
  setup() {
    onBeforeMount(async () => await clickStore.init())
    const inc = () => {
      clickStore.incrementCount()
      // should throw a warning and don't mutate the store
      clickStore.getState().count++
    }
    return {
      countState: clickStore.getState(),
      isInitialized: clickStore.getIsInitialized(),
      inc
    }
  }
}
</script>