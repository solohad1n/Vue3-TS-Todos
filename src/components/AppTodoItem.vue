<template>
  <li class="todo-item" :class="{'todo-item--done': todo.completed}" @click="toggleTogo">
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
import { defineComponent, PropType } from "vue";
import { Todo } from '@/types/Todo'

export default defineComponent({
  props: {
    todo: {
      type: Object as PropType<Todo>,
      required: true
    }
  },
  methods: {
    toggleTogo () {
      this.$emit('toggleTogo', this.todo.id)
    },
    removeTodo () {
      this.$emit('removeTodo', this.todo.id)
    }
  },
  emits: {
    toggleTogo: (id: number) => Number.isInteger,
    removeTodo: (id: number) => Number.isInteger
  }
})
</script>