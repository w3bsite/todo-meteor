<template>
  <div class="my-4">
    <div class="container">
      <form class="new-task row" @submit.prevent="handleSubmit">
        <div class="my-1 mx-auto col-12 col-sm-8 col-md-8">
          <textarea
            type="text-area"
            placeholder="Type to add new tasks"
            v-model="newTask"
            class="form-control my-1 mx-auto"
          />
        </div>
        <!--  -->
        <!--  -->
        <button
          class="btn btn-secondary my-auto mx-auto col-12 col-sm-4 col-md-2"
          type="submit"
        >
          Add Task
        </button>
      </form>
    </div>
  </div>
</template>

<script>
import { TasksCollection } from "../../api/collections/TasksCollection";

export default {
  data() {
    return {
      newTask: "",
    };
  },
  methods: {
    handleSubmit(event) {
      TasksCollection.insert({
        text: this.newTask,
        createdAt: new Date(), // current time
      });

      // Clear form
      this.newTask = "";
    },
  },
};
</script>