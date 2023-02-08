<template>
  <ul class="todo-list" >
    <li class="todo-list-item" :data-index="todo.id"
        v-for="(todo, index) in todos"
        :key="todo.id"
        :data-id="index"
        draggable="true"
        @dragstart="dragStart"
        @dragend="dragEnd"
        @dragover.prevent="dragOver"
        @drop.prevent="drop($event, this)"
        @dragleave="dragLeave"
        :class="{'todo-list-item__status--finished' : todo.completed }"
    >
      <div
        class="todo-list-item__status"
        @click="finishTodo(todo.id)"
        @keyup.space="finishTodo"
      >
        <img src="../assets/images/icon-check.svg" alt="">
      </div>
      <h2 class="todo-list-item__heading">
        {{ todo.title }}
      </h2>
    </li>
  </ul>
</template>

<script>

export default {
  components: {
  },
  props: ['todos'],
  setup(props, context) {
    const finishTodo = (id) => {
      context.emit('finish-todo', id);
    };

    /* eslint-disable no-param-reassign */
    const swapArrayLocs = (arr, index1, index2) => {
      [arr[index1], arr[index2]] = [arr[index2], arr[index1]];
    };

    const dragStart = (e) => {
      e.dataTransfer.setData('text/plain', e.target.getAttribute('data-id'));
      console.log(e.target.getAttribute('data-id'));
      e.currentTarget.classList.add('dragging');
    };

    const drop = (e) => {
      e.currentTarget.classList.remove('drag-over');
      const idFrom = e.dataTransfer.getData('text/plain');
      const idTo = e.currentTarget.getAttribute('data-id');
      swapArrayLocs(props.todos, idFrom, idTo);
    };

    const dragEnd = (e) => {
      e.currentTarget.classList.remove('dragging');
    };

    const dragOver = (e) => {
      e.currentTarget.classList.add('drag-over');
    };

    const dragLeave = (e) => {
      e.currentTarget.classList.remove('drag-over');
    };

    return {
      finishTodo,
      dragStart,
      dragEnd,
      drop,
      dragOver,
      dragLeave,
    };
  },
};
</script>

<style scoped>
.todo-list {
  margin-top: 24px;
  background-color: #fff;
  border-radius: 5px;
  list-style: none;
  display: flex;
  flex-direction: column;
}

.todo-list-item {
  display: flex;
  align-items: center;
  gap: 24px;
  padding: 20px 24px;
  border-bottom: 1px solid #E3E4F1;
  cursor: grab;
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

.todo-list-item__status--finished div {
  background: linear-gradient(to right, #55DDFF 0%, #C058F3);
}

.todo-list-item__status--finished h2 {
  text-decoration: line-through;
}

.todo-list-item__heading {
  font-size: 18px;
  font-weight: normal;
}

.drag-over {
  border: 1px dashed black;
}

.dragging {
  cursor: grabbing;
}
</style>
