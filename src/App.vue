<template>
  <div id="app">
    <h1><b-icon-document-text></b-icon-document-text>Simple task list</h1>
    <NewTask @taskAdded="addTask" />
    <TaskGrid :tasks="tasks"
      @taskDeleted="deleteTask"
      @taskStateChanged="toggleTaskState" />
    <hr>
    <TasksProgress :progress="progress" />
  </div>
</template>

<script>
  import TaskGrid from "./components/TaskGrid"
  import NewTask from "./components/NewTask"
  import TasksProgress from "./components/TasksProgress"
  export default {
    name: "App",
    components: { TaskGrid, NewTask, TasksProgress },
    data() {
      return {
        tasks: []
      }
    },
    computed: {
      progress() {
        const total = this.tasks.length
        const done = this.tasks.filter(t => !t.pending).length
        return Math.round(done / total * 100) || 0
      }
    },
    watch: {
      tasks: {
        deep: true,
        handler() {
          localStorage.setItem('tasks', JSON.stringify(this.tasks))
        }
      }
    },
    methods: {
      addTask(task) {
        const sameName = t => t.name === task.name
        const reallyNew = this.tasks.filter(sameName).length == 0
        if(reallyNew) {
          this.tasks.push({
            name: task.name,
            pending: task.pending || true
          })
        }
      },
      deleteTask(i) {
        this.tasks.splice(i, 1)
      },
      toggleTaskState(i) {
        this.tasks[i].pending = !this.tasks[i].pending
      }
    },
    created() {
      const json = localStorage.getItem('tasks')
      const array = JSON.parse(json) || []
      this.tasks = Array.isArray(array) ? array : []
    }
  }
</script>

<style lang="scss">
  @font-face {
    font-family: "RobotoMono";
    src: url("./assets/fonts/RobotoMono-Thin.ttf");
  }
  * {
    font-family: "RobotoMono", monospace;
  }
  body {
    margin: 0;
    h1 {
      font-weight: bold;
    }
    #app {
      display: flex;
      flex-direction: column;
      height: 100vh;
      align-items: center;
      color: white;
      background: #012933;
      padding-top: 60px;
    }
  }
</style>
