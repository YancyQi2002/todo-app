<template>
  <div
      class="flex items-center m-2 p-1 w-6/12 bg-white rounded-md shadow-md border-4"
      :class="completed?'border-green-500' : 'border-white'"
      style="margin-left: 8.5rem"
  >
    <div class="flex-shrink-0 m-2 ml-2 align-middle">
      <input
          type="checkbox"
          :checked="completed"
          @change="toggleCompletion()"
      />
    </div>
    <div class="ml-1">
      <h4 class="text-xl text-gray-900 leading-tight">{{ task }}</h4>
    </div>
  </div>
</template>

<script>
import {defineComponent,onMounted} from 'vue'
import {useStore} from '@/store'
import {MutationType} from '@/store/mutations'

export default defineComponent({
  name: "TodoItem",
  props: {
    id: {type: Number, required: true},
    task: {type: String, required: true},
    completed: {type: Boolean, required: true}
  },
  setup(props) {
    onMounted(()=>{
      console.log('TodoItem')
    })
    const store = useStore()
    const toggleCompletion = () => {
      store.commit(MutationType.CompleteItem, {
        id: props.id,
        completed: !props.completed
      })
    }

    return {
      toggleCompletion
    }
  }

})
</script>

<style scoped>

</style>