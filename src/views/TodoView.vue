<template>
  <TheHeader />
  <TheInput @add-todo="addTodo" />
  <TheTodoList :todos="filteredTodos" @finish-todo="finishTodo" />
  <TheTodoAction
    :todos="filteredTodos"
    @change-filter="filterTodos"
    @clear-completed="clearCompleted"
  />
</template>

<script>
import TheHeader from '@/components/TheHeader.vue';
import TheInput from '@/components/TheInput.vue';
import TheTodoList from '@/components/TheTodoList.vue';
import TheTodoAction from '@/components/TheTodoAction.vue';
import { reactive, ref } from 'vue';

export default {
  name: 'HomeView',
  components: {
    TheTodoAction,
    TheInput,
    TheHeader,
    TheTodoList,
  },

  setup() {
    let todos = reactive([
      {
        id: 1,
        title: 'Learn Vue.js',
        completed: true,
      },
      {
        id: 2,
        title: 'Setup Some Hotkeys',
        completed: false,
      },
      {
        id: 3,
        title: 'Learn Redux',
        completed: false,
      },
      {
        id: 4,
        title: 'Begin to look at Angular',
        completed: false,
      },
    ]);
    const filteredTodos = ref(todos);

    const filterTodos = (filterBy) => {
      if (filterBy === 'all') {
        filteredTodos.value = todos;
      } else if (filterBy === 'active') {
        filteredTodos.value = todos.filter((todo) => !todo.completed);
      } else if (filterBy === 'completed') {
        filteredTodos.value = todos.filter((todo) => todo.completed);
      }
    };

    const addTodo = (todoToAdd) => {
      todos.push({
        id: todos.length + 1,
        title: todoToAdd,
        completed: false,
      });
      filterTodos('all');
    };

    const finishTodo = (id) => {
      filteredTodos.value.forEach((todo) => {
        if (todo.id === id) {
          /* eslint-disable no-param-reassign */
          todo.completed = !todo.completed;
        }
      });
    };

    const clearCompleted = () => {
      todos = todos.filter((todo) => !todo.completed);
      filteredTodos.value = todos;
    };

    return {
      todos,
      addTodo,
      finishTodo,
      filteredTodos,
      filterTodos,
      clearCompleted,
    };
  },
};
</script>
