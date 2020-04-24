<template>
  <AppDrop @drop="moveTaskOrColumn">
    <AppDrag
      class="column"
      :transferData="{
            type: 'column',
            fromColumnIndex: columnIndex
          }"
    >
      <div class="flex items-center mb-2 font-bold">{{ column.name }}</div>
      <Task
        v-for="(task, $taskIndex) of column.tasks"
        :key="$taskIndex"
        :board="board"
        :task="task"
        :taskIndex="$taskIndex"
        :column="column"
        :columnIndex="columnIndex"
      />

      <input
        type="text"
        class="block p-2 w-full bg-transparent"
        placeholder="+ Enter new task"
        @keyup.enter="createTask($event, column.tasks)"
      />
    </AppDrag>
  </AppDrop>
</template>

<script>
import Task from "./Task.vue";
import AppDrag from "./AppDrag.vue";
import AppDrop from "./AppDrop.vue";
import MoveTaskOrColumnMixin from "@/mixins/MoveTaskOrColumnMixin";

export default {
  components: {
    Task,
    AppDrag,
    AppDrop
  },
  mixins: [MoveTaskOrColumnMixin],
  methods: {
    createTask(e, tasks) {
      this.$store.commit("CREATE_TASK", { tasks, name: e.target.value });
      // clear the input
      e.target.value = "";
    },
    pickupColumn(e, columnIndex) {
      e.dataTransfer.effectAllowed = "move";
      e.dataTransfer.dropEffect = "move";
      e.dataTransfer.setData("from-column-index", columnIndex);
      e.dataTransfer.setData("type", "column");
    }
  }
};
</script>

<style>
.column {
  @apply bg-grey-light p-2 mr-4 text-left shadow rounded;
  min-width: 350px;
}
</style>