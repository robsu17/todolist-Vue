<template>
  <div class="bg-gray-300 rounded-sm mb-2">
    <div class="flex items-center px-4 py-3 border-b
border-gray-400 last:border-b-0">
      <div class="flex items-center justify-center
mr-2">
        <button :class="(todo.completed || todoCompleted) ? 'text-green-500' : 'text-gray-500'" @click="completedAction()">
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24"
               xmlns="http://www.w3.org/2000/svg">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M5 13l4 4L19 7"></path>
          </svg>
        </button>
      </div>

      <div class="w-full">
        <input type="text" v-model="nameTask" @focusout="updateName()" :class="['bg-gray-300 placeholder-gray-500\n'+
'text-gray-700 font-light focus:outline-none block w-full appearance-none\n'+
'leading-normal mr-3', (todo.completed || todoCompleted) ? 'line-through' : '']">
      </div>

      <div class="ml-auto flex items-center
justify-center">
        <button class="focus:outline-none" @click="removeItem()">
          <svg class="ml-3 h-4 w-4 text-gray-500 hover:text-red-600" viewBox="0 0 24 24" fill="none" stroke="currentColor"
               xmlns="http://www.w3.org/2000/svg">
            <path d="M19 7L18.1327 19.1425C18.0579
20.1891 17.187 21 16.1378 21H7.86224C6.81296 21 5.94208 20.1891 5.86732
19.1425L5 7M10 11V17M14 11V17M15 7V4C15 3.44772 14.5523 3 14 3H10C9.44772
3 9 3.44772 9 4V7M4 7H20" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"/>
          </svg>
        </button>
      </div>
    </div>
  </div>
</template>
<script>

import axios from "axios";

export default {
  name: 'TodoItem',
  data() {
    return {
      todoCompleted: false,
      nameTask: this.todo.title
    }
  },
  props: {
    todo: {
      type: Object,
      required: true
    }
  },
  methods: {
    completedAction() {
      axios.patch(`http://localhost:3000/todos/${this.todo.id}`, {
        completed: true
      }).then(() => {
        this.todoCompleted = true
      })
    },

    removeItem() {
      this.$emit('remItem', this.todo.id)
    },

    updateName() {
      axios.patch(`http://localhost:3000/todos/${this.todo.id}`, {
        title: this.nameTask
      })
    }
  }
}
</script>