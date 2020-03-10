<template>
  <div>
    <div class="new-task">
      <input v-model="name" @keydown.enter="add" type="text"
        class="form-element" placeholder="New task">
      <button class="form-element" @click="add">+</button>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        name: ''
      }
    },
    methods: {
      add() {
        this.$emit('taskAdded', { name: this.name })
        this.name = ''
      }
    },
  }
</script>

<style lang="scss" scoped>
  @import '../assets/scss/variables.scss';
  .new-task {
    margin: 10px 0 60px;
    .form-element {
      outline: none;
      font-size: 1rem;
      border: solid 1px $gray;
      padding: 10px 15px;
      color: $white;
    }
    input {
      font-weight: bold;
      width: 500px;
      background: transparent;
      border-top-left-radius: 8px;
      border-bottom-left-radius: 8px;
      &::placeholder {
        color: $gray;
      }
    }
    button {
      border-left: none;
      background-color: $blue;
      border-top-right-radius: 8px;
      border-bottom-right-radius: 8px;
    }
  }
</style>