<template>
  <footer class="app-footer">{{ stats.activeCount }} more to do, {{ stats.doneCount }} done</footer>
</template>
<script lang="ts">
import { defineComponent, type PropType } from 'vue'
export interface Stats {
  activeCount: number
  doneCount: number
}
export default defineComponent({
  props: {
    stats: {
      type: Object as PropType<Stats>,
      required: true
    }
  }
})
</script>
