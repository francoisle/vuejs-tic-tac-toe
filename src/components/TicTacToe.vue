<template>
  <div>
    <GameStatus v-bind:playNumber="playNumber" :isOver="isOver"/>
    <Board v-bind:grid="grid" @square:clicked="handleGridClick" :isOver="isOver"/>
  </div>
</template>

<script>
  import GameStatus from './GameStatus';
  import Board from './Board';

  export default {
    components: {
      GameStatus,
      Board
    },

    data: function () {
      return {
        playNumber: 0,
        grid: [
          ['', '', ''],
          ['', '', ''],
          ['', '', '']
        ],
      }
    },

    methods: {
      handleGridClick(rowIndex, columnIndex) {
        const row = this.grid[rowIndex].slice();
        row[columnIndex] = (this.playNumber % 2 === 0) ? 'X' : 'O';
        this.grid.splice(rowIndex, 1, row);
        this.playNumber++;
      }
    },

    computed: {
      isOver() {
        const lines = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6]
        ];

        return lines.some(line => {
          const [a, b, c] = line;
          return (
            this.grid[Math.trunc(a / 3)][a % 3] !== '' &&
            this.grid[Math.trunc(a / 3)][a % 3] === this.grid[Math.trunc(b / 3)][b % 3] &&
            this.grid[Math.trunc(a / 3)][a % 3] === this.grid[Math.trunc(c / 3)][c % 3]
          );
        })
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
