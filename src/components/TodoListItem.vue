<template>
  <li
    class="list-group-item"
    :class="{ 'list-group-item-success': todoItem.completed }"
  >
    <input
      type="checkbox"
      :checked="todoItem.completed"
      @change="$emit('toggle-completed', todoItem.id)"
    />
    <span :class="{ 'todo-done': todoItem.completed }">
      {{ todoItem.todo }}
      {{ todoItem.completed ? '(완료)' : '' }}
    </span>

    <span
      class="float-end badge bg-secondary"
      @click.stop="$emit('delete-todo', todoItem.id)"
      >삭제</span
    >
  </li>
</template>

<script>
export default {
  name: 'TodoListItem',
  props: {
    todoItem: { type: Object, required: true },
  },
  emits: ['toggle-completed', 'delete-todo'],
};
</script>
```
