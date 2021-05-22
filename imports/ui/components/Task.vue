<template>
  <div
    class="px-5"
    :class="{
      ' note note-success text-muted': !!task.checked,
      'note note-info': !task.checked,
    }"
  >
    <div class="row">
      <div class="col custom-control custom-checkbox align-self-end">
        <input
          type="checkbox"
          readOnly
          :checked="!!task.checked"
          @click="toggleChecked"
          class="custom-control-check-input"
          value=""
          id="flexCheckDefault"
        />
        <label class="col-11" for="flexCheckDefault">
          {{ this.task.text }}
        </label>
      </div>
      <button
        class="delete btn btn-outline-danger btn-rounded mdb-chips col-12 col-sm-1"
        @click="deleteThisTask"
        style="max-height: 36px"
      >
        X
      </button>
    </div>
  </div>
</template>

<script>
import { TasksCollection } from "../../api/collections/TasksCollection";
export default {
  props: ["task"],
  data() {
    return {};
  },
  computed: {
    taskClassName: function () {
      return this.task.checked ? "checked" : "";
    },
  },
  methods: {
    deleteThisTask() {
      TasksCollection.remove(this.task._id);
    },
    toggleChecked() {
      // Set the checked property to the opposite of its current value
      TasksCollection.update(this.task._id, {
        $set: { checked: !this.task.checked },
      });
    },
  },
};
</script>
