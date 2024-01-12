<template>
  <div id="app">
    <AppHeader/>
    <AppFilters/>
    <main class="app-main">
      <AppTodolist/>
      <AppAddTodo/>
    </main>
    <AppFooter/>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import AppFilters from './components/AppFilters.vue';
import AppHeader from './components/AppHeader.vue';
import AppTodolist from './components/AppTodolist.vue';
import AppAddTodo from './components/AppAddTodo.vue';
import AppFooter from './components/AppFooter.vue';


export default defineComponent({
  name: 'App',
  components: {
    AppHeader,
    AppFilters,
    AppTodolist,
    AppAddTodo,
    AppFooter
  }
});
</script>
