<template>
  <aside class="app-filters">
    <section class="toggle-group">
      <button
        v-for="filter in filters"
        class="button"
        :class="{ 'button--primary': filter === activeFilter }"
        @click="setActiveFilter(filter)"
      >
        {{ filter }}
      </button>
    </section>
  </aside>
</template>
<script lang="ts">
import type { Filter } from '@/types/Filter'
import { defineComponent, type Prop, type PropType } from 'vue'

interface State {
  filters: Filter[]
}

export default defineComponent({
  props: {
    activeFilter: {
      type: String as PropType<Filter>,
      required: true
    }
  },
  data(): State {
    return {
      filters: ['All', 'Active', 'Completed']
    }
  },
  methods: {
    setActiveFilter(filter: Filter): void {
      this.$emit('update:activeFilter', filter)
    }
  },
  emits: {
    'update:activeFilter': (filter: Filter) => filter
  }
})
</script>
