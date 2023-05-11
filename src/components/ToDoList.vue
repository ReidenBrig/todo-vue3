<template>
  <div class="todo__box" v-for="(todo,i) in todos" :key="todo.id">
    <p>
      <span class="todo__id">{{ i + 1 }}.</span>
      <span
          class="todo__text"
          :class="{todo__text_isShow: todo.isComplete}">
            {{ todo.text }}
          </span>
      <input @change="isDoneItem" v-model="todo.isComplete" type="checkbox"/>
      <span class="todo__delete" @click="removeItem(i)">x</span>
    </p>

  </div>
</template>

<script>
import {defineComponent} from 'vue'
export default defineComponent({

  props: ['todos', 'removeTodo', 'isDoneTodo'],
  setup() {
    function removeItem(index) {
      this.$emit('removeTodo', index)
    }
    function isDoneItem() {
      this.$emit('isDoneTodo')

    }
    return {
      removeItem,
      isDoneItem
    }


  },
/*  methods: {
    removeItem(index) {
      this.$emit('removeTodo', index)
    },
    isDoneItem() {
      this.$emit('isDoneTodo')

    }
  }*/
})
</script>

<style scoped>

</style>