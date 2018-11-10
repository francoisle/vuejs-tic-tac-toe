<template>
  <div class=container>
    <div class="row" v-for="(row, rowIndex) of grid" :key="rowIndex">
      <div class="square" v-for="(square, squareIndex) of row" :key="squareIndex"
           v-on:click="handleSquareClick(rowIndex, squareIndex)">
        {{square}}
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      grid: Array,
      isOver: Boolean
    },

    methods: {
      handleSquareClick(rowIndex, squareIndex) {
        if (this.isOver) {
          return;
        }

        if (this.grid[rowIndex][squareIndex] !== '') {
          return;
        }

        this.$emit('square:clicked', rowIndex, squareIndex);
      }
    }
  }
</script>

<style scoped>
  .container {
    margin: 25px;
    display: inline-block;
  }

  .row {
    display: table;
    clear: both;
    content: "";
  }

  .square {
    background: #fff;
    border: 1px solid #999;
    float: left;
    font-size: 24px;
    font-weight: bold;
    line-height: 34px;
    height: 34px;
    margin-right: -1px;
    margin-top: -1px;
    padding: 0;
    text-align: center;
    width: 34px;
    user-select: none;
  }
</style>