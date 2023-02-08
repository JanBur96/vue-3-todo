<template>
  <form class="new-todo" @keydown.enter.prevent="addTodo">
    <div class="new-todo__ring"></div>
    <label for="newTodo">
      <input
        class="new-todo__input"
        type="text"
        id="newTodo"
        aria-label="Create a new todo"
        placeholder="Create a new todo..."
        v-model="title"
      />
    </label>
  </form>
</template>

<script>
import { ref } from 'vue';

export default {
  setup(props, context) {
    const title = ref('');

    const addTodo = () => {
      context.emit('add-todo', title.value);
      title.value = '';
    };

    return { title, addTodo };
  },
};
</script>

<style scoped>
.new-todo {
  margin-top: 2.5rem;
  height: 64px;
  background-color: #ffffff;
  display: flex;
  align-items: center;
  padding: 20px 24px;
  gap: 24px;
  border-radius: 5px;
}

.new-todo__ring {
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 100%;
  border: 1px solid #E3E4F1;
}

.new-todo__input {
  border: none;
  font-family: inherit;
  font-size: 18px;
  outline: none;
}
</style>
