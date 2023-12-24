<template>
  <div class="px-3 py-10 md:px-10">
    <div class="w-full sm:w-1/2 lg:w-1/3 mx-auto">
      <TodoFormAdd v-on:nameTodo="itemAdd" />

      <TodoItems :todosArray="todos" v-on:listAtt="atualizaLista"/>

      <TodoEmpty v-if="todos.length === 0"/>
    </div>
  </div>
</template>

<script>
import TodoFormAdd from "@/components/TodoFormAdd.vue";
import TodoEmpty from "@/components/TodoEmpty.vue";
import TodoItems from "@/components/TodoItems.vue";
import axios from "axios";

export default {
  name: 'App',
  components: {
    TodoItems,
    TodoEmpty,
    TodoFormAdd,
  },
  data() {
    return {
      todos: [{}]
    }
  },
  created() {
    axios.get('http://localhost:3000/todos')
        .then((response) => {
          this.todos = response.data
        })
  },
  methods: {
    itemAdd(todo) {
      axios.post('http://localhost:3000/todos', todo)
          .then((response) => {
            this.todos.push(response.data)
          })
    },
    atualizaLista(listaAtt) {
      this.todos = listaAtt
    }
  }
}
</script>

<style>

</style>
