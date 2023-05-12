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
  props: {
    todos: {
      type: [Object, Array],
      required: true
    },
    removeTodo: {
      type: Function,
      required: true
    },
    isDoneTodo: {
      type: Function,
      required: true
    }

  },

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
})
</script>

<style scoped>

</style>