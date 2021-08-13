<template>
  <div class="to-do-list">

    <ul v-if="room.todos.length > 0">
      <li v-for="todo in room.todos" v-bind:key="todo.priority">
        {{todo.priority + 1}}&nbsp;
        <span class="to-do-item" :style="{ backgroundColor: todo.hexColor }">
          {{ todo.value }}
        </span>
        <span class="close-button" @click="removeToDo(todo.priority)">&times;</span>
      </li>
    </ul>

    <p v-else>There are no ToDos yet. Add one now!</p>

    <input id="todoInput" type="text" v-model="todoInput" @keyup.enter="addToDo">
    <button @click="addToDo">Add ToDo</button>

    <p class="input-error" v-for="error in todoInputErrors" :key="error">{{ error }}</p>

  </div>
</template>

<script lang="ts">
  import { defineComponent } from 'vue'

  export default defineComponent({
    name: 'ToDoList',
    props: ['room'],
    data(){
      return {
        todoInput: '',
        todoInputErrors: [],
      }
    },
    methods: {
      addToDo() {
        this.todoInputErrors = []

        // Validate todo input
        if(!this.todoInput) {
          this.todoInputErrors.push('You need to provide an input!')
          return
        } 

        var todo = {
          priority: this.room.todos.length,
          value: this.todoInput,
          hexColor: this.getRandomHexColor(),
        }
        this.$emit('addToDo', todo)
        this.todoInput = ''
      },

      removeToDo(todoPriority: Number) {
        this.$emit('removeToDo', todoPriority)
      },

      getRandomHexColor() {
        var letters = '0123456789ABCDEF'
        var color = '#'
        for (var i = 0; i < 6; i++) {
          var generatedIndex = Math.floor(Math.random() * 16)
          if(i < 3 && generatedIndex < 8) {
            generatedIndex = 8
          }
          color += letters[generatedIndex]
        }
        return color
      }
    }
  });
</script>

<style scoped>
  .input-error {
    color: indianred;
  }

  div.to-do-list ul {
    list-style: none;
  }

  div.to-do-list ul li {
    margin: 20px;
    cursor: move;
  }

  span.to-do-item {
    border: 2px solid darkslategray;
    border-radius: 5px;
    padding: 5px;
  }
  
  span.close-button {
    position: relative;
    font-size: 1.6em;
    top: 4px;
  }
  span.close-button:hover {
    color: red;
    cursor: pointer;
  }
</style> 