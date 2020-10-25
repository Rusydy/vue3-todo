<template>
  <h1>Vue 3 Todo</h1>

  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add</button>
  </form>

    <div>
      <button @click="markAllDone()">Mark All Done</button>
      <button @click="removeAll()">Remove All Done</button>
    </div>

  <ul>
    <li v-for="(todo, index) in todos" 
    :key="todo.id"
    >
      <h3 
      class="todo"
      :class="{ done: todo.done }"
      @click="toggleDone(todo)"
      >{{ todo.content }}</h3>
      <div>
        <!-- <button @click="toggleDone(todo)">DONE</button> -->
        <button @click="removeTodo(index)">Remove</button>
      </div>
    </li>
  </ul>
</template>

<script>
import { ref } from 'vue'

export default {
  setup() {
    const newTodo = ref('')
    const todos = ref([])

    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      })
      newTodo.value = ''
    }

    function toggleDone(todo) {
      todo.done = !todo.done
    }

    function removeTodo(index) {
      todos.value.splice(index, 1)
    }

    function markAllDone() {
      todos.value.forEach((todo) => todo.done = !todo.done)
    }

    function removeAll() {
      todos.value.length = 0
    }

    return {
      todos,
      newTodo,
      toggleDone,
      addNewTodo,
      removeTodo,
      markAllDone,
      removeAll,
    }
  }
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Quicksand:wght@600&display=swap");
$colomn-color: #0706446b;
$first-width: 500px;
$second-width: 350px;

#app {
  font-family: "Quicksand", sans-serif;
  text-align: center;
  color: #1f2225;
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

form {
  background: $colomn-color;
  display: flex;
  font-size: 1em;
  align-items: center;
  justify-content: space-evenly;
  width: $first-width;
  margin: 1rem;
  padding: 2rem;
  border-radius: 2rem;
}

ul{
  list-style-type: none;
  background: $colomn-color;
  border-radius: 2rem;
  
  li{
    margin-top: 2px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: $first-width;

    .todo{
      cursor: pointer;
    }
    
    button{
      display: flex;
      margin: 13px;
    }
  }
}

.done{
  text-decoration: line-through;
}

@media (max-width: 604px) {
  form{
    display: flex;
    flex-direction: column;
    justify-items: center;
    width: $second-width;
    margin: 1rem;

    input{
      margin: 1rem;
    }
  }

  ul{
    li{
      width: $second-width;
      border-radius: 1rem;
    }
  }
}
</style>
