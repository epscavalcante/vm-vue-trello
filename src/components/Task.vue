<template>
  <AppDrop @drop="moveTaskOrColumn">
    <AppDrag
      class="task"
      :transferData="{
        type: 'task',
        fromColumnIndex: columnIndex,

        fromTaskIndex: taskIndex
      }"
      @click="goToTask(task)"
    >
      <span class="w-full flex-no-shrink font-bold">{{ task.name }}</span>
      <p v-if="task.description" class="w-full flex-no-shrink mt-1 text-sm">
        {{ task.description }}
      </p>
    </AppDrag>
  </AppDrop>
</template>

<script>
import MoveTaskOrColumnMixin from "@/mixins/MoveTaskOrColumnMixin";
import AppDrag from "@/components/AppDrag";
import AppDrop from "@/components/AppDrop";

export default {
  components: {
    AppDrop,
    AppDrag
  },
  mixins: [MoveTaskOrColumnMixin],
  props: {
    task: {
      type: Object,
      required: true
    },
    taskIndex: {
      type: Number,
      required: true
    }
  },
  methods: {
    goToTask(task) {
      console.log("helow");
      this.$router.push({ name: "task", params: { id: task.id } });
    }
  }
};
</script>

<style lang="scss" scoped>
</style>