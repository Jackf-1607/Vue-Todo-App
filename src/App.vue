<template>
  <div class="container text-left">
    <h1>Todo List</h1>
    <form @submit.prevent="addNewTodo">
        <div class="mb-3">
          <label for="newTodo" class="form-label ">New Todo</label>
          <input v-model="newTodo" type="text" class="form-control" id="newTodo" name="newTodo">
        </div>
        <button type="submit" class="btn btn-primary">Submit</button>
      </form>

      <button class="markAll btn btn-success" @click="markAllDone">Mark All Done</button>
      <button class="markAll btn btn-primary" @click="markAllNotDone">Un Mark All Done</button>
      <button class="markAll btn btn-danger" @click="removeAllTodos">Remove All</button>

      <ul class="">
        <li v-for="(todo, index ) in todos" :key="todo.id" class="todo">
          <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">{{ todo.content }}</h3>
          <button @click="removeTodo(index)" class="btn btn-danger remove">Remove Todo</button>
        </li>
      </ul>
</div>
</template>

<script>
import { ref } from 'vue'

export default {
  setup(){
    const newTodo = ref('')
    const todos= ref([])

    function addNewTodo(){
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      })
      newTodo.value = '' //Clear value on form submit
    }

    function toggleDone(todo){
      todo.done = !todo.done
    }

    function removeTodo(index){
      todos.value.splice(index, 1)
    }

    function markAllDone(){
      todos.value.forEach((todo) => todo.done = true);
    }

    function markAllNotDone(){
      todos.value.forEach((todo) => todo.done = false);
    }

    function removeAllTodos(){
      todos.value = [];
    }

    return{
      todos,
      newTodo,
      addNewTodo,
      toggleDone,
      removeTodo,
      markAllDone,
      markAllNotDone,
      removeAllTodos,
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
}

.done{
  text-decoration: line-through;
}

.todo{
  cursor: pointer;
}

.markAll{
  margin: 15px 0 15px 0;
}

.remove{
  margin-bottom: 10px;
}
</style>
