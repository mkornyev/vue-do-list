<template>
  <div id="app">
    <NavHeader :header="header" :taglines="taglines"/>

    <div v-if="room === null">
      <RoomEntryForm @loadRoom="loadToDoRoom"/>
    </div>

    <div v-else>
      <ToDoList :room="room" @addToDo="addToDo"/>
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
      taglines: ['To get started, join or create a room below.'],
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
    }
  },
});
</script>
