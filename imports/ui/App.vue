<template>
  <div class="container card">
    <header class="card-header my-4">
      <h3 class="card-title text-center">Todo List</h3>

      <TaskForm />
    </header>
    <div class="d-flex flex-column card-body">
      <Task class="my-2" v-for="task in tasks" :key="task._id" :task="task" />
    </div>
  </div>
</template>


<script>
import Task from "./components/Task.vue";
import { TasksCollection } from "../api/collections/TasksCollection";
import TaskForm from "./components/TaskForm.vue";

export default {
  components: {
    Task,
    TaskForm,
  },
  data() {
    return {};
  },
  methods: {},
  meteor: {
    tasks() {
      return TasksCollection.find({}, { sort: { createdAt: -1 } }).fetch();
    },
  },
};
</script>