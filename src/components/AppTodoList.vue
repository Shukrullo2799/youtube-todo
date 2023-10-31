<template>
  <ul class="todo-list">
    <app-todo-item
      v-for="todo in todos"
      :key="todo.id"
      :todo="todo"
      @toggle-todo="toggleTodo"
      @remove-todo="removeTodo"
    />
  </ul>
</template>
<script lang="ts">
import { defineComponent, type PropType } from 'vue'
import AppTodoItem from './AppTodoItem.vue'
import type { Todo } from '@/types/Todo'

export default defineComponent({
  components: {
    AppTodoItem
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>,
      required: true
    }
  },
  emits: {
    'toggle-todo': (id: number) => Number.isInteger(id),
    'remove-todo': (id: number) => Number.isInteger(id)
  },
  methods: {
    toggleTodo(id: number): void {
      this.$emit('toggle-todo', id)
    },
    removeTodo(id: number): void {
      this.$emit('remove-todo', id)
    }
  }
})
</script>
