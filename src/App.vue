<template>
  <div id="app">
    <AppHeader/>
    <AppFilters
    :active-filter="activeFilter"
    @set-filter="setFilter"
    />
    <main class="app-main">
      <AppTodolist
      :todos="filterdTodos"
      @remove-todo="removeTodo"
      @toggle-togo="toggleTodo"
      />
      <AppAddTodo
      @add-todo="addTodo"
      />
    </main>
    <AppFooter :stats="stats"/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppFilters from './components/AppFilters.vue';
import AppHeader from './components/AppHeader.vue';
import AppTodolist from './components/AppTodolist.vue';
import AppAddTodo from './components/AppAddTodo.vue';
import AppFooter from './components/AppFooter.vue';
import { Todo } from './types/Todo';
import { Filter } from '@/types/Filter';
import { Stats } from '@/types/Stats';

interface State {
  todos: Todo[],
  activeFilter: Filter
}

export default defineComponent({
  name: 'App',
  components: {
    AppHeader,
    AppFilters,
    AppTodolist,
    AppAddTodo,
    AppFooter
  },
  data(): State {
    return {
      todos: [
        {
        id: 0,
        text: 'Learn the basics of Vue',
        completed: true
        },
        {
        id: 1,
        text: 'Learn the basics of Typescript',
        completed: false
        },
        {
        id: 2,
        text: 'Subscribe to the channel',
        completed: false
        }
      ],
      activeFilter: 'All'
    }
  },
  computed: {
    filterdTodos(): Todo[] {
      switch (this.activeFilter) {
        case 'Active':
          return this.activeTodos
        case 'Done':
          return this.doneTodos
        case 'All':
        default: 
          return this.todos
      }
    },
    activeTodos(): Todo[] {
      return this.todos.filter(todo => !todo.completed)
    },
    doneTodos(): Todo[] {
      return this.todos.filter(todo => todo.completed)
    },
    stats(): Stats {
      return {
        active: this.activeTodos.length,
        done: this.doneTodos.length
      }
    }
  },
  methods: {
    addTodo(todo: Todo) {
      this.todos.push(todo)
    },
    toggleTodo(id: number) {
      //Находит объект по заданному id и меняет значение true на false и наоборот
      const targetTodo = this.todos.find((todo: Todo) => todo.id === id)
      
      if (targetTodo) {
        targetTodo.completed = !targetTodo.completed
      }
    },
    removeTodo(id: number) {
      //Находит объект по заданному id и удаляет его переписывая наш массив todos
      this.todos = this.todos.filter((todo: Todo) => todo.id !== id)
    },
    setFilter(filter: Filter) {
      this.activeFilter = filter
    }
  }
});
</script>
