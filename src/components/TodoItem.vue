<script setup>
import { Icon } from "@iconify/vue";
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
  index: {
    type: Number,
    required: true,
  },
});

const emit = defineEmits(["toggle-completed", "toggle-edit", "update-todo", "delete-todo"]);

</script>


<template>
  <li class="todo-item">
    <input type="checkbox" :checked="todo.isCompleted" @input="$emit('toggle-completed', props.index)" />
    <div class="todo-text">
      <input v-if="todo.isEditing" type="text" :value="todo.todo" v-on:change="$emit('update-todo', $event.target.value, index)" />
      <h3 v-else :class="{strike: todo.isCompleted}">{{ todo.todo }}</h3>
    </div>
    <Icon  icon="ph:pencil-bold" v-show="!todo.isEditing" @click="$emit('toggle-edit', props.index)" />
    <Icon icon="material-symbols:delete-outline-sharp" @click="$emit('delete-todo', todo.id)" />
  </li>
</template>

<style lang="scss" scoped>
.todo-item{
  display: flex;
  background-color: #e9e9e9;
  margin-top: 5px;
  padding: 10px;
  border-radius: 5px;

  .strike {
      text-decoration: line-through;
  }
  .todo-text {
    flex-grow: 1;

    h3{
      margin-top: 0;
      margin-bottom: 0;
    }
  }

}
</style>