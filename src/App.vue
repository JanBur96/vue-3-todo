<template>
  <TheContainer>
    <TodoView />
  </TheContainer>
</template>

<script>
import TheContainer from '@/components/TheContainer.vue';
import TodoView from './views/TodoView.vue';

export default {
  components: {
    TheContainer,
    TodoView,
  },
};
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #444;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
