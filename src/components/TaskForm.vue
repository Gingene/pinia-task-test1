<template lang="">
  <form @submit.prevent="handerSubmit">
    <input type="text" placeholder="I need to..." v-model="newTask" />
    <button>Add</button>
  </form>
</template>
<script>
import { ref } from "vue";
import { useTaskSotre } from "../stores/TaskStore";
export default {
  setup() {
    const TaskStore = useTaskSotre();

    const newTask = ref("");

    const handerSubmit = () => {
      if (newTask.value.length > 0) {
        TaskStore.addTask({
          title: newTask.value,
          isFav: false,
          id: Date.now() + Math.floor(Math.random() * 100),
        });
      }
      newTask.value = "";
    };

    return { handerSubmit, newTask };
  },
};
</script>
<style>
.new-task-form {
  background-color: #e7e7e7;
  padding: 20px 0;
}
form {
  max-width: 400px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: 3fr 1fr;
  gap: 10px;
}
form button {
  background-color: #ffd859;
  border: 0;
  border-radius: 6px;
  color: #555;
  font-size: 1rem;
}
</style>
