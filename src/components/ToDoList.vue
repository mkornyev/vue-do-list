<template>
  <div class="to-do-list">

    
    <ul v-if="room.todos.length > 0">
      <li v-for="todo in room.todos" v-bind:key="todo.priority">
        {{todo.priority + 1}}&nbsp;<span class="to-do-item">{{ todo.value }}</span>
      </li>
    </ul>

    <p v-else>There are no ToDo's yet. Add one now!</p>

    <input id="todoInput" type="text" v-model="todoInput">
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
          hexColor: '000000',
        }
        this.$emit('addToDo', todo)
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
</style> 