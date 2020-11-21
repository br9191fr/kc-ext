<template>
  <div v-if="isInitialized">
    <button @click="inc()">Clicked is really new now {{ countState.count }} times.</button>
  </div>
</template>
// new test
// a comment in test branch
// another comment
//in test 2 first
//in test 2 second
// final in master
// a new comment in test branch
// fianl add
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