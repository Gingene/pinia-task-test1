<template lang="">
  <main>
    <!-- heading -->
    <header>
      <img src="./assets/pinia-logo.svg" alt="pinia logo" />
      <h1>Pinia Tasks</h1>
    </header>

    <!-- new task form -->
    <div class="new-task-form">
      <TaskForm />
    </div>

    <!-- filter -->
    <nav class="filter">
      <button @click="filter = 'all'">All tasks</button>
      <button @click="filter = 'favs'">Fav tasks</button>
    </nav>

    <!-- loading -->
    <div class="loading" v-if="loading">Loading tasks...</div>

    <!-- task list -->
    <div class="task-list" v-if="filter === 'all'">
      <p>Your have {{ totalCount }} tasks left to do</p>
      <div v-for="task in tasks">
        <TaskDetails :task="task" />
      </div>
    </div>

    <div class="task-list" v-if="filter === 'favs'">
      <p>Your have {{ favCount }} favs left to do</p>
      <div v-for="task in favs">
        <TaskDetails :task="task" />
      </div>
    </div>

    <button @click="taskStore.$reset">reset state</button>
  </main>
</template>
<script>
import { ref } from "vue";
import TaskDetails from "./components/TaskDetail.vue";
import TaskForm from "./components/TaskForm.vue";
import { useTaskSotre } from "./stores/TaskStore";
import { storeToRefs } from "pinia";
export default {
  components: { TaskDetails, TaskForm },
  setup() {
    const taskStore = useTaskSotre();

    // const { tasks, loading, favs, totalCount, favCount } =
    //   storeToRefs(taskStore);
    const myRefs = storeToRefs(taskStore);

    // fetch
    taskStore.getTasks();

    const filter = ref("all");

    return { taskStore, filter, ...myRefs };
  },
};
</script>
<style lang="css">
.filter {
  width: 640px;
  margin: 10px auto;
  text-align: right;
}

.filter button {
  display: inline-block;
  margin-left: 10px;
  background-color: #fff;
  border: 2px solid #555;
  border-radius: 4px;
  padding: 4px 8px;
  cursor: pointer;
  font-size: 1rem;
}

.loading {
  max-width: 640px;
  border: 1px solid #ffe9a0;
  color: #3a3a3a;
  padding: 5px 0;
  text-align: center;
  margin: 30px auto;
}
</style>
