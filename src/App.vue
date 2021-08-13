<template>
  <div id="app">
    <NavHeader :header="header" :taglines="taglines"/>

    <div v-if="room === null">
      <RoomEntryForm @loadRoom="loadToDoRoom"/>
    </div>

    <div v-else>
      <ToDoList :room="room" @addToDo="addToDo" @removeToDo="removeToDo"/>
    </div>
  </div>
</template>

<script lang="ts">
// IMPORTS 
import { defineComponent } from 'vue';
import NavHeader from './components/NavHeader.vue'
import RoomEntryForm from './components/RoomEntryForm.vue'
import ToDoList from './components/ToDoList.vue'
import './App.css'


// INTERFACES 
interface ToDoItem {
  priority: Number,
  value: String, 
  hexColor: String,
}

interface Room {
  id: String,
  name: String,
  todos: [ToDoItem?],
}


// COMPONENT
export default defineComponent({
  name: 'App',
  components: {
    NavHeader, 
    RoomEntryForm,
    ToDoList,
  },
  data() {
    return {
      header: 'Welcome to the Vue-Do list!',
      taglines: ['A live collaborative todo tool.', 'To get started, join or create a room below.'],
      room: null,
    }
  },
  methods: {
    loadToDoRoom(room: Room) {
      console.log(`Loading room #${room.id}, ${room.name}`)

      this.room = room
      this.header = this.room.name
      this.taglines = [`Room ID: ${this.room.id}`]
    },

    addToDo(todo: ToDoItem) {
      if(this.room) {
        this.room.todos.push(todo)
      }
    },

    removeToDo(todoPriority: Number) {
      let newToDos = this.room.todos.filter((todo: ToDoItem) => {
        return todo.priority != todoPriority
      })
      var index = -1
      this.room.todos = newToDos.map((todo: ToDoItem) => {
        index += 1
        return { priority: index, value: todo.value, hexColor: todo.hexColor }
      })
    }
  },
});
</script>
