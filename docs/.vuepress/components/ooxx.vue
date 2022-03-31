<template>
      <div class="game">
        <div class="game-board">
            <div> <button @click="resetBoard()">Reset</button>
                <div class="board-row" v-for="row in 3" :key="'r'+row">
                    <button class="square" v-for="col in 3" :key="'c'+row+col" @click="put(row-1, col-1)">
                        {{ board[row-1][col-1] }}
                    </button>
                </div>
            </div>
        </div>
        <div class="game-info">
        </div>
      </div>
</template>

<script>
export default {
    data() {
        return {
            board: null,
            current: 'O',
        }
    },
    created() {
        this.resetBoard()
    },
    methods: {
        resetBoard() {
            this.board = [['','',''],['','',''],['','','']]
            this.current = 'O'
        },
        put(row, col) {
            if (this.board[row][col] !== '') return
            this.board[row][col] = this.current
            this.$set(this.board, row, this.board[row])
            this.current = (this.current == 'O') ? 'X' : 'O'
        },
    }
}
</script>

<style scoped>
.board-row:after {
  clear: both;
  content: "";
  display: table;
}

.square {
  background: #fff;
  border: 2px solid #999;
  float: left;
  font-size: 48px;
  font-weight: bold;
  line-height: 68px;
  height: 68px;
  margin-right: -1px;
  margin-top: -1px;
  padding: 0;
  text-align: center;
  width: 68px;
}

.square:focus {
  outline: none;
}

</style>