<template>
  <section class="add-todo">
    <form v-if="isVisible" class="add-todo__form" @submit.prevent="sendTodo">
      <button class="close-button" type="button" @click="hideForm">
        <i class="bi bi-x"></i>
      </button>
      <div class="text-input text-input--focus">
        <input v-model="todoText" class="input" />
      </div>
      <button class="button button--filled">Add task</button>
    </form>
    <button v-else class="add-todo__show-form-button" @click="showForm">
      <i class="bi bi-plus-lg"></i>
    </button>
  </section>
</template>
<script lang="ts">
import type { Todo } from '@/types/Todo'
import { defineComponent } from 'vue'

interface State {
  isVisible: boolean
  todoText: string
}

export default defineComponent({
  data(): State {
    return {
      isVisible: false,
      todoText: ''
    }
  },
  methods: {
    showForm(): void {
      this.isVisible = true
    },
    hideForm(): void {
      this.isVisible = false
    },
    sendTodo(): void {
      this.$emit('add-todo', {
        id: Date.now(),
        text: this.todoText,
        completed: false
      })
      this.todoText = ''
      this.hideForm()
    }
  },
  emits: {
    'add-todo': (item: Todo) => item
  }
})
</script>
