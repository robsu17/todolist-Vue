<template>
  <div class="space-y-2" :key="todo.id" v-for="todo in todosArray">
    <TodoItem :todo="todo" />
  </div>
</template>
<script>
import TodoItem from "@/components/TodoItem.vue";

export default {
  name: 'TodoItems',
  components: {
    TodoItem
  },
  props: {
    todosArray: {
      type: Array,
      required: true
    }
  }
}
</script>