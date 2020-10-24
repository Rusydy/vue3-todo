<template>
  <h1>Vue 3 Todo</h1>

  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo">
    <button>Add</button>
  </form>

  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <h3>{{ todo.content }}</h3>
      <div>
        <button>text</button>
        <button>text</button>
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
    }

    return {
      todos,
      newTodo,
      addNewTodo,
    }
  }
}
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Quicksand:wght@600&display=swap");
$colomn-color: #ffa3a330;
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
    
    button{
      display: flex;
      margin: 13px;
    }
  }
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
