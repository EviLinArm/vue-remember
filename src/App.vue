<template>
  <div>
    <h1 class="h1">Remember me?</h1>
    <p>Запомни и открой все зеленые клетки</p>

    <Board/>
  </div>
</template>

<script>
import Board from './components/Board.vue'
export default {
  name: 'App',
  components: {
    Board,
  }
}

</script>

<style scoped>

</style>
