<template>
  <div class="row">
    <div class="col">
      <ul class="list-group">
        <li class="list-group-item">
          <strong> 할일 목록 </strong>
          <span
            v-if="props.count >= 2"
            class="float-end badge btn btn-success"
            @click="$emit('delete-all')"
          >
            전체삭제
          </span>
        </li>
        <TodoListItem
          v-for="todoItem in todoList"
          :key="todoItem.id"
          :todoItem="todoItem"
          @toggle-completed="$emit('toggle-completed', $event)"
          @delete-todo="$emit('delete-todo', $event)"
        />
      </ul>
    </div>
  </div>
</template>
<script>
import TodoListItem from './TodoListItem.vue';

export default {
  name: 'TodoList',
  components: { TodoListItem },
  props: {
    todoList: { type: Array, required: true },
    count: { type: Number, required: true },
  },
  emits: ['toggle-completed', 'delete-todo', 'delete-all'],
};
</script>
