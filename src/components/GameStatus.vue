<template>
  <div>
    <span v-if="!isOver">
      Next Player: {{currentPlayer}}
    </span>
    <span v-else>
      Player: {{previousPlayer}} won the game !
    </span>
  </div>
</template>

<script>
  export default {
    props: {
      playNumber: Number,
      isOver: Boolean
    },

    computed: {
      previousPlayer() {
        return (this.playNumber % 2 === 0) ? 'O' : 'X';
      },
      currentPlayer() {
        return (this.playNumber % 2 === 0) ? 'X' : 'O';
      }
    }
  }
</script>

<style scoped>

</style>
