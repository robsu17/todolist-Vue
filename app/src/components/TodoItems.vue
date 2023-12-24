<template>
  <div class="space-y-2" :key="todo.id" v-for="todo in todosArray">
    <TodoItem :todo="todo" v-on:remItem="itemRemove"/>
  </div>
</template>
<script>
import TodoItem from "@/components/TodoItem.vue";
import axios from "axios";

export default {
  name: 'TodoItems',
  emits: ['listAtt'],
  components: {
    TodoItem
  },
  props: {
    todosArray: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      listaAtt: [{}]
    }
  },
  methods: {
    itemRemove(id) {
      axios.delete(`http://localhost:3000/todos/${id}`)
          .then(() => {
            this.$emit('listAtt', this.todosArray.filter((todo) => todo.id !== id))
          })
    }
  }
}
</script>