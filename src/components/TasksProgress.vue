<template>
  <div class="tasks-progress">
    <span class="progress-value">{{ progress }}%</span>
    <div class="progress-bar" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<script>
  export default {
    props: {
      progress: { type: Number, default: 0 }
    }
  }
</script>

<style lang="scss" scoped>
  @import '../assets/scss/variables.scss';
  .tasks-progress {
    position: absolute;
    bottom: 5%;
    width: 80%;
    border: solid 1px $gray;
    color: $white;
    border-radius: 12px;
    margin-bottom: 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
    .progress-bar {
      position: absolute;
      border-radius: 12px;
      height: 100%;
      background: rgb(3,55,96);
      background: linear-gradient(90deg, rgba(3,55,96,1) 0%, rgba(33,150,243,1) 100%);
      align-self: flex-start;
    }
    .progress-value {
      z-index: 1;
      font-size: .6rem;
      font-weight: bold;
      padding: 3px 0;
    }
  }
</style>