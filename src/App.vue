<script lang="ts">
import { defineComponent } from 'vue'
import AppHeader from './components/AppHeader.vue'
import AppFilter from './components/AppFilter.vue'
import AppTodoList from './components/AppTodoList.vue'
import AppAddTodo from './components/AppAddTodo.vue'
import AppFooter, { type Stats } from './components/AppFooter.vue'
import type { Todo } from '@/types/Todo'
import type { Filter } from '@/types/Filter'

interface State {
  todos: Todo[]
  activeFilter: Filter
}

export default defineComponent({
  name: 'App',
  components: {
    AppHeader,
    AppFilter,
    AppTodoList,
    AppAddTodo,
    AppFooter
  },
  data(): State {
    return {
      todos: [
        { id: 1, text: 'Learn the basics of Vue', completed: true },
        { id: 2, text: 'Learn the basics of Typescript', completed: false },
        { id: 3, text: 'Subscribe to the channel', completed: false }
      ],
      activeFilter: 'All'
    }
  },
  computed: {
    filteredTodo(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos
        case 'Completed':
          return this.completedTodos
        default:
          return this.todos
      }
    },
    stats(): Stats {
      return {
        activeCount: this.activeTodos.length,
        doneCount: this.completedTodos.length
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => !todo.completed)
    },
    completedTodos(): Todo[] {
      return this.todos.filter((todo: Todo) => todo.completed)
    }
  },

  methods: {
    addTodo(todo: Todo): void {
      this.todos.push(todo)
    },
    toggleTodo(id: number): void {
      this.todos = this.todos.map((todo: Todo) =>
        todo.id === id ? { ...todo, completed: !todo.completed } : todo
      )
    },
    removeTodo(id: number): void {
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    }
  }
})
</script>

<template>
  <div id="app">
    <app-header />
    <app-filter v-model:active-filter="activeFilter" />
    <main class="app-main">
      <app-todo-list :todos="filteredTodo" @remove-todo="removeTodo" @toggle-todo="toggleTodo" />
      <app-add-todo @add-todo="addTodo" />
    </main>
    <app-footer :stats="stats" />
  </div>
</template>
