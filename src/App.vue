<template>
  <div id="app">
    <h1 class="title">
      {{ state.title }}
    </h1>
    <div class="todo">
      <input v-model="state.todo" type="text" placeholder="type todo..."/>
      <button @click="addTodo">Add todo</button>
      <to-do-list :todos="state.todos" @removeTodo="removeTodo" @isDoneTodo="isDoneTodo"/>
      <hr>
      <p>
        Список задач: {{ state.todos.length }}
      </p>
    </div>
  </div>
</template>

<script setup>

import ToDoList from "@/components/ToDoList";
import {v4 as uuidv4} from 'uuid';
import {onMounted, reactive } from 'vue'

const state = reactive ({
  title: 'ToDo app',
  todo: '',
  todos: [],
  isComplete: false,
  id: null,
})

function addTodo() {

  if (state.todo != '') {
    console.log(state.todos)
    state.todos.push({
      id: uuidv4(),
      text: state.todo,
      isComplete: false,
    })

    localStorage.setItem('todos', JSON.stringify(state.todos))
  }

  state.todo = '';
}

function isDoneTodo() {
  localStorage.setItem('todos', JSON.stringify(state.todos))

}

function removeTodo(index) {
  state.todos.splice(index, 1);
  localStorage.setItem('todos', JSON.stringify(state.todos))
}

onMounted(() => {
  const data = localStorage.getItem('todos');
  data ? state.todos = JSON.parse(data) : null;
})

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.title {
  text-align: center;
}

.todo {
  margin: 0 auto;
  padding: 30px;
  width: 500px;
  height: 100%;
  background-color: #dcd9d9;
  //outline: 1px solid black;
  border-radius: 10px;
  min-height: 500px;

  &__box {
    margin-top: 10px;
    min-width: 250px;
    border: #2c3e50 1px solid;
    border-radius: 10px;
  }

  &__id {
    color: #2c3e50;
  }

  &__text {
    font-size: 15px;
    color: #2c3e50;
    text-transform: capitalize;

    &_isShow {
      color: grey;
      text-decoration: line-through;
    }
  }

  &__delete {
    padding: 0 5px;
    border: 1px solid #2c3e50;
    border-radius: 3px;
    margin-right: 10px;
    float: right;
  }

}

</style>
