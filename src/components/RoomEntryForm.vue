<template>
  <div class="room-entry">

    <label for="roomCode">10 Digit Room Code:</label>
    <input id="roomCode" type="text" v-model="roomIdInput">

    <button class="btn btn-lg" @click="enterRoom">Join Room</button>

    <br/>

    <label for="roomName">Room Name:</label>
    <input id="roomName" type="text" v-model="nameInput">

    <button class="btn btn-lg" @click="createRoom">Create Room</button>

    <!-- <input v-bind:showRoom="isRoomLoaded" v-on:input="$emit('loadRoom', $event.target.value)"> -->
  </div>
</template>

<script lang="ts">
  import { defineComponent } from 'vue';
  import ToDoItem from '../App.vue'

  export default defineComponent({
    name: 'RoomEntryForm',
    data(){
      return {
        roomIdInput: '',
        nameInput: '',
      }
    },
    methods: {
      createRoom() {
        // Create a room for the given name 
        var room = { 
          id: '18dsn93grv', // generate ID
          name: this.nameInput,
          todos: [] as typeof ToDoItem[]
        }

        this.$emit('loadRoom', room)
      },
      enterRoom() {
        // Validate roomID 
        var room = { 
          id: this.roomIdInput, 
          name: 'an existing room',
          todos: [] as typeof ToDoItem[]
        }
        this.$emit('loadRoom', room)
      }
    }
  });
</script>
