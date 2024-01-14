<template>
  <ul class="todo-list">
    <AppToloItem
    v-for="todo in todos"
    :key="todo.id"
    :todo="todo"
    @toggle-togo="toggleTogo"
    @remove-todo="removeTodo"
    />
  </ul>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue";
import AppToloItem from './AppTodoItem.vue'
import { Todo } from '@/types/Todo'

export default defineComponent({
  components: {
    AppToloItem
  },
  props: {
    todos: {
      type: Array as PropType<Todo[]>
    }
  },
  methods: {
    toggleTogo(id: number) {
      this.$emit('toggleTogo', id)
    },
    removeTodo(id: number) {
      this.$emit('removeTodo', id)
    }
  },
  emits: {
    toggleTogo: (id: number) => Number.isInteger,
    removeTodo: (id: number) => Number.isInteger
  }
})
</script>