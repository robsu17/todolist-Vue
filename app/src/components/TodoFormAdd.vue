<template>
  <form class="flex items-center px-4 bg-gray-900 h-15
rounded-sm border-l-2 border-green-400 mb-3">
    <input placeholder="Adicione um novo item ..." v-model="name" type="text" class="bg-gray-900 placeholder-gray-500 text-gray-500
font-light focus:outline-none block w-full appearance-none leading-normal
py-3 pr-3">

    <button
        :class="['text-green-400 hover:text-green-300 text-xs font-semibold focus:outline-none duration-200',
         { 'disabled': name.length === 0, 'opacity-50': name.length === 0}]"
        type="submit"
        @click.prevent="adicionarItem()"
        :disabled="name.length === 0"
    >
      ADICIONAR
    </button>
  </form>
</template>

<script>

export default {
  name: 'TodoFormAdd',
  data() {
    return {
      name: ''
    }
  },
  methods: {
    adicionarItem() {
      this.$emit('nameTodo', {
        title: this.name,
        completed: false
      })
      this.name = ''
    }
  }
}
</script>