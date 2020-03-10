<template>
  <div class="task-grid">
    <template v-if="tasks.length">
      <Task v-for="(task, i) in tasks" :key="task.name"
        @taskDeleted="$emit('taskDeleted', i)"
        @taskStateChanged="$emit('taskStateChanged', i)"
        :task="task" />
    </template>
    <p v-else class="no-task"><b-icon-heart-fill></b-icon-heart-fill> Suas tarefas estão em dia!</p>
  </div>
</template>

<script>
  import Task from "./Task";
  export default {
    components: { Task },
    props: {
      tasks: { type: Array, required: true }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../assets/scss/variables.scss';
  .task-grid {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    .task {
      margin: 10px;
    }
    .no-task {
      color: $gray;
      font-size: 1.5rem;
      svg {
        color: $bg-pending;
      }
    }
  }
</style>
