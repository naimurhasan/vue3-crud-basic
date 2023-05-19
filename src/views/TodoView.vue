<script setup>
import {ref, watch} from "vue";
import {uid} from "uid"
import TodoCreator from '../components/TodoCreator.vue';
import TodoItem from '../components/TodoItem.vue';
import { computed } from "@vue/reactivity";

const totdoList = ref([

]);


const fetchTodoList = () => {
  const tl = localStorage.getItem("todoList");
  if (tl) {
    totdoList.value = JSON.parse(tl);
  }
}

fetchTodoList();

const setLocalStorage = () => {
  console.log("setLocalStorage");
  localStorage.setItem("todoList", JSON.stringify(totdoList.value));
}


watch(totdoList, setLocalStorage, {deep: true});

const createTodo = (todo) => {
  totdoList.value.push({
    id: uid(),
    todo,
    isCompleted: false,
    isEditing: false,
  });
};

const toggleCompleted = (index) => {
    totdoList.value[index].isCompleted = !totdoList.value[index].isCompleted;
};

const toggleEdit = (index) => {
    totdoList.value[index].isEditing = !totdoList.value[index].isEditing;
};

const updateTodo = (value, index) => {
    totdoList.value[index].todo = value;
    totdoList.value[index].isEditing = false;
};

const deleteTodo = (id) => {
  totdoList.value = totdoList.value.filter((todo) => todo.id !== id);
};

const countComputed = computed(() => {
  return totdoList.value.length;
});

</script>

<template>
  <div>
    <TodoCreator @create-todo="createTodo" :count="countComputed" />
    <ul class="todo-unorderd-list">
      <TodoItem v-for="(todo, index) in totdoList" :todo="todo" :index="index" @delete-todo="deleteTodo" @update-todo="updateTodo" @toggle-completed="toggleCompleted" @toggle-edit="toggleEdit"/>
    </ul>
    <p class="text-center" v-show="!countComputed">You don't have any todo :(</p>
  </div>
</template>

<style lang="scss" scoped>
  .todo-unorderd-list {
    list-style: none;
    max-width: 400px;
    margin: auto;
}

.text-center {
    text-align: center;
}

</style>