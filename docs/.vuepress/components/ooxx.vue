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
            step: 0,
            from: "",
        }
    },
    created() {
        this.resetBoard()
        console.log("Board", this.board)
    },
    methods: {
        resetBoard() {
            this.board = [['','',''],['','',''],['','','']]
            this.current = 'O'
            this.step = 0
        },
        move(row, col) {
            if (this.from === '' && this.board[row][col] === '') return
            if (this.from !== '' && this.board[row][col] !== '') {
                this.from = row*3 + col
                return
            }
            this.step += 1
            if (this.from === '') return this.from = row*3 + col
            let frow = Math.floor(this.from/3)
            this.board[row][col] = this.board[frow][this.from%3]
            this.board[frow][this.from%3] = ''
            this.$set(this.board, row, this.board[row])
            this.$set(this.board, frow, this.board[frow])
            this.from = ''
        },
        put(row, col) {
            if (this.step >= 6) return this.move(row, col)
            if (this.board[row][col] !== '') return
            this.step += 1
            this.board[row][col] = (this.step % 2 === 1) ? 'O' : 'X'
            this.$set(this.board, row, this.board[row])
            console.log("B", this.board)
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