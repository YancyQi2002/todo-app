<template>
  <div class="container mt-0 mx-auto p-0 h-screen bg-blue-200 overflow-y-auto">
    <h1 class="text-3xl text-center mt-10 p-2 font-bold">TodoList</h1>
    <h2 class="text-3xl text-center p-2 font-bold">采用 Vue3.0 + Typescript + Vuex 4 + TailwindCSS 1.8.11</h2>
    <div v-if="loading">
      <h3>Loading...</h3>
    </div>
    <div v-else>
      <p class="text-center mt-2">{{ completedCount }} / {{ totalCount }} 完成</p>
      <AddTodoItem />
      <TodoList />
    </div>
  </div>
  <router-view />
</template>

<script lang="ts">
import { defineComponent, computed, onMounted } from "vue";
import AddTodoItem from "./components/AddTodoItem.vue";
import TodoList from "./components/TodoList.vue";
import { useStore } from "./store";
import { ActionTypes } from "./store/actions";

export default defineComponent({
  components: { TodoList, AddTodoItem },
  setup() {
    const store = useStore();
    const loading = computed(() => store.state.loading);
    onMounted(() => {
      console.log("App...");
      store.dispatch(ActionTypes.GetTodoItems);
    });

    const completedCount = computed(() => store.getters.completedCount);
    const totalCount = computed(() => store.getters.totalCount);

    return { loading, completedCount, totalCount };
  },
});
</script>