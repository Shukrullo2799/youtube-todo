<template>
  <li class="todo-item" :class="{ 'todo-item--done': todo.completed }" @click="toggleTodo">
    <div class="todo-item__status">
      <i class="bi bi-check2"></i>
    </div>
    <span class="todo-item__text">{{ todo.text }}</span>
    <button class="todo-item__remove-button" @click.stop="removeTodo">
      <i class="bi bi-trash3"></i>
    </button>
  </li>
</template>
<script lang="ts">
import { type PropType, defineComponent } from 'vue'
import type { Todo } from '@/types/Todo'

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true
    }
  },
  emits: {
    'toggle-todo': (id: number) => Number.isInteger(id),
    'remove-todo': (id: number) => Number.isInteger(id)
  },
  methods: {
    toggleTodo(): void {
      this.$emit('toggle-todo', this.todo.id)
    },
    removeTodo(): void {
      this.$emit('remove-todo', this.todo.id)
    }
  }
})
</script>
