<script setup>
import {reactive} from "vue"

const todoState = reactive({
  todo: "Testing"
})
</script>

<template>
  <div class="container">
    <h1>Create Todo</h1>
    <div class="input-wrap">
      <input name="todo" type="text" v-model="todo" placeholder="Enter Todo" />
      <button>Add Todo</button>
    </div>
  </div>
</template>



<style lang="scss" scoped>
.container{
  text-align: center;

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