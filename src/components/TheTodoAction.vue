<template>
  <div class="todo-action">
    <div>
      <p>{{ todos.length }} Item(s) left</p>
    </div>
    <ul class="todo-action__selected">
      <li
        @click="selectFilter('all')"
        @keyup.space="selectFilter('all')"
        class="todo-action__selected-item"
        :class="{'todo-action__selected-item--active' : activeFilter === 'all'}">
        All
      </li>
      <li
        @click="selectFilter('active')"
        @keyup.space="selectFilter('active')"
        class="todo-action__selected-item"
        :class="{'todo-action__selected-item--active' : activeFilter === 'active'}">
        Active
      </li>
      <li
        @click="selectFilter('completed')"
        @keyup.space="selectFilter('completed')"
        class="todo-action__selected-item"
        :class="{'todo-action__selected-item--active' : activeFilter === 'completed'}">
        Completed
      </li>
    </ul>
    <p>Clear Completed</p>
  </div>
  <p class="todo-action__info">Drag and drop to reorder list</p>
</template>

<script>
import { ref } from 'vue';

export default {
  props: ['todos'],
  setup(props, context) {
    const activeFilter = ref('all');

    const selectFilter = (filterToSelect) => {
      activeFilter.value = filterToSelect;
      context.emit('change-filter', filterToSelect);
    };

    return {
      selectFilter,
      activeFilter,
    };
  },
};
</script>

<style scoped>
.todo-action {
  padding: 20px 24px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #fff;
}

.todo-action__selected {
  display: flex;
  align-items: center;
  list-style: none;
  gap: 18px;
  font-size: 14px;
}

.todo-action__selected-item {
  font-weight: bold;
  cursor: pointer;
}

.todo-action__selected-item--active {
  color: #3A7CFD;
}

.todo-action__info {
  margin-top: 48px;
  text-align: center;
}
</style>
