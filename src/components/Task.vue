<template>
  <div class="task" :class="stateClass">
    <span title="Done" @click="$emit('taskStateChanged', task)" class="check-task">
      <b-icon-check></b-icon-check>
    </span>
    <span title="Delete" @click="$emit('taskDeleted', task)" class="delete-task">
      <b-icon-trash></b-icon-trash>
    </span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
  export default {
    props: {
      task: { type: Object, required: true }
    },
    computed: {
      stateClass() {
        return {
          pending: this.task.pending,
          done: !this.task.pending
        };
      }
    }
  };
</script>

<style lang="scss" scoped>
  @import '../assets/scss/variables.scss';
  .task {
    box-sizing: border-box;
    min-width: 250px;
    min-height: 100px;
    padding: 10px;
    border-radius: 8px;
    font-size: 1.2rem;
    font-weight: bold;
    user-select: none;
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    p {
      margin: 0;
    }
    &.pending {
      border-left: 12px solid $border-pending;
      background-color: $bg-pending;
      p {
        color: $border-pending;
      }
      .delete-task, .check-task {
        background-color: $border-pending;
        &:hover {
          background-color: $hover-pending;
        }
      }
    }
    &.done {
      color: $text-done;
      border-left: 12px solid $border-done;
      background-color: $bg-done;
      p {
        color: $border-done;
        position: relative;
        opacity: .5;
        &:before {
          content: '';
          height: 1px;
          width: 100%;
          background-color: $border-done;
          position: absolute;
          bottom: 40%;
        }
      }
      .delete-task,.check-task {
        background-color: $border-done;
        &:hover {
          background-color: $hover-done;
        }
      }
    }
    .delete-task, .check-task {
      cursor: pointer;
      position: absolute;
      top: 5px;
      font-size: 1rem;
      font-weight: bold;
      height: 20px;
      width: 20px;
      border-radius: 10px;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .delete-task { right: 5px; }
    .check-task { right: 30px; }
  }
</style>
