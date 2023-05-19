<script setup>
import {reactive} from "vue"

const props = defineProps({
  count: {
    type: Number,
    required: true,
  },
})

const emit = defineEmits(["create-todo"])

const todoState = reactive({
  todo: "",
  invalid: false,
  errMsg: "",
})

const createTodo = () => {
  if(todoState.todo==""){
    todoState.invalid = true
    todoState.errMsg = "Please enter a todo"
    return
  }
  emit("create-todo", todoState.todo)
  todoState.todo = ""
  todoState.invalid = false
  todoState.errMsg = ""
}

</script>

<template>
  <div class="container">
    <h1>Create Todo <span v-show="count">{ {{ count }} }</span></h1>
    <div class="input-wrap">
      <input name="todo" type="text" v-model="todoState.todo" placeholder="Enter Todo" />
      <button @click="createTodo()">Add Todo</button>
    </div>
    <p v-show="todoState.invalid" class="error">{{todoState.errMsg}}</p>
  </div>
</template>



<style lang="scss" scoped>
.container{
  text-align: center;

  .error{
    color: red;
  }

  .input-wrap{
    display: flex;
    justify-content:center ;
    gap: 12px;
    margin-top: 12px;

    input{
      padding: 8px 12px;
      border: 1px solid #ccc;
      border-radius: 4px;
      outline: none;
    }

    button{
      padding: 8px 12px;
      border: 1px solid #ccc;
      border-radius: 4px;
      outline: none;
      background-color: #ccc;
      cursor: pointer;
    }
  }
}
</style>