<template>
  <div class="w mx-4">
    <form class="my-4" @submit.prevent="addTodoItem">
      <div class="flex items-center bg-white p-1 rounded-md shadow-md" style="margin-left: 25%;">
        <div class="flex-grow m-1 ml-3">
          <input
              v-model="todo"
              type="text"
              class="w-full focus:outline-none"
              placeholder="添加一个任务吧!"
          />
        </div>
        <div class="flex-shrink-0">
          <button
              type="submit"
              class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-3 rounded"
          >
            添加
          </button>
        </div>
      </div>
    </form>
  </div>
</template>

<script lang="ts">
import {defineComponent, ref} from 'vue'
import {useStore} from '@/store'
import {TodoItem} from "@/store/state"
import {MutationType} from "@/store/mutations"

export default defineComponent({
  name: "AddTodoItem",
  setup() {
    const todo = ref('')
    const store = useStore()

    const addTodoItem = () => {
      if (todo.value === '') {
        return
      }
      const item: TodoItem = {
        id: Date.now(),
        task: todo.value,
        completed: false
      }
      store.commit(MutationType.CreateItem, item)
      todo.value = ''
    }
    return {
      addTodoItem,
      todo
    }
  }
})
</script>

<style scoped>
  .w {
    width: 80%;
  }
</style>