<template>
  <li class="todo-list-item" :data-index="todo.id"
      v-for="(todo, index) in todos"
      :key="todo.id" :todo="todo" :data-id="index"
      @finish-todo="finishTodo"
      draggable="true"
      @dragstart="dragStart"
      @dragend="dragEnd"
      @dragover.prevent="dragOver"
      @dragenter.prevent
      @drop.prevent="drop($event, this)"
      @dragleave="dragLeave"
  >
    <div
      class="todo-list-item__status"
      @click="finishTodo"
      @keyup.space="finishTodo"
      :class="{'todo-list-item__status--finished' : todo.completed }"
    >
      <img src="../assets/images/icon-check.svg" alt="">
    </div>
    <h2 class="todo-list-item__heading">
      {{ todo.title }}
    </h2>
  </li>
</template>

<script>
export default {
  props: ['todo', 'index'],
  setup(props, context) {
    const finishTodo = () => {
      context.emit('finish-todo', props.todo.id);
    };

    return { finishTodo };
  },
};
</script>

<style scoped>
.todo-list-item {
  display: flex;
  align-items: center;
  gap: 24px;
  padding: 20px 24px;
  border-bottom: 1px solid #E3E4F1;
}

.todo-list-item__status {
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 100%;
  border: 1px solid #E3E4F1;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.todo-list-item__status--finished {
  background: linear-gradient(to right, #55DDFF 0%, #C058F3);
}

.todo-list-item__heading {
  font-size: 18px;
  font-weight: normal;
}
</style>
