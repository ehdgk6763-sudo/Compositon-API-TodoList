<template>
  <div id="app" class="container">
    <div class="card card-body bg-dark text-white">
      <div class="title">🕒 TodolistApp 💻</div>
    </div>
    <div class="card card-body">
      <div class="row text-center">
        <div class="col">전체 todo 개수: {{ totalCount }}</div>
        <div class="col">
          완료 todo 개수:
          {{ completedCount }}
        </div>
        <div class="col">
          미완료 todo 개수:
          {{ notCompletedCount }}
        </div>
      </div>
    </div>
    <div class="card card-default card-borderless">
      <div class="card-body">
        <InputTodo @add-todo="addTodo" />
        <TodoList
          :todoList="todoList"
          :count="count"
          @toggle-completed="toggleCompleted"
          @delete-todo="deleteTodo"
          @delete-all="deleteAll"
        />
      </div>
    </div>
  </div>
</template>

<script>
import InputTodo from './components/InputTodo.vue';
import TodoList from './components/TodoList.vue';
import { ref, computed } from 'vue';

let ts = new Date().getTime();

export default {
  name: 'App',
  components: { TodoList, InputTodo },
  setup() {
    const todoList = ref([
      { id: ts, todo: 'Vue 원고 집필', completed: false },
      { id: ts + 1, todo: '일요일 애견 카페', completed: false },
      { id: ts + 2, todo: '자전거타기', completed: false },
      { id: ts + 3, todo: '딸과공원산책', completed: true },
      { id: ts + 4, todo: '실습 문제 풀기', completed: true },
    ]);

    const count = ref(0);

    const totalCount = computed(() => todoList.value.length);

    const completedCount = computed(
      () => todoList.value.filter((item) => item.completed === true).length,
    );

    const notCompletedCount = computed(
      () => todoList.value.filter((item) => item.completed === false).length,
    );
    const toggleCompleted = (id) => {
      let index = todoList.value.findIndex((item) => id === item.id);
      todoList.value[index].completed = !todoList.value[index].completed;
      count.value += todoList.value[index].completed ? 1 : 0;
    };

    const deleteTodo = (id) => {
      let index = todoList.value.findIndex((item) => id === item.id);
      todoList.value.splice(index, 1);
    };
    const addTodo = (todo) => {
      if (todo.length >= 2) {
        todoList.value.push({
          id: new Date().getTime(),
          todo: todo,
          completed: false,
        });
      }
    };
    const deleteAll = () => {
      if (confirm('정말로 삭제하시겠습니까?')) {
        todoList.value = [];
      }
    };
    return {
      todoList,
      totalCount,
      completedCount,
      notCompletedCount,
      toggleCompleted,
      deleteTodo,
      addTodo,
      deleteAll,
    };
  },
};
</script>
