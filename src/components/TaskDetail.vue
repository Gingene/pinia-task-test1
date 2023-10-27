<template lang="">
  <div class="task">
    <h3>{{ task.title }}</h3>
    <div class="icons">
      <i class="material-icons" @click="taskStore.deleteTask(task.id)"
        >delete</i
      >
      <i
        class="material-icons"
        :class="{ active: task.isFav }"
        @click="taskStore.toggleFav(task.id)"
        >favorite</i
      >
    </div>
  </div>
</template>
<script>
import { useTaskSotre } from "../stores/TaskStore";
export default {
  props: ["task"],
  setup() {
    const taskStore = useTaskSotre();

    return { taskStore };
  },
};
</script>
<style lang="css">
.task-list {
  max-width: 640px;
  margin: 20px auto;
}

.task {
  padding: 6px 20px;
  background-color: #fff;
  margin-top: 20px;
  border-radius: 4px;
  box-shadow: 2px 4px 6px rgba(0, 0, 0, 0.05);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.task h3,
.task .icons {
  display: inline-block;
}

.task,
.icons {
  text-align: right;
}

.task i {
  font-size: 1.4rem;
  margin-right: 6px;
  cursor: pointer;
  color: #bbb;
}

.task i.active {
  color: #ff005d;
}
</style>
