<template>
  <mdb-container fluid class="fill">
    <mdb-row class="fill">
      <mdb-col class="padawan-board">
        <mdb-col class="centered">
          <h2 style="color:#ff7e00">Padawan's Board</h2>
          <Board />
        </mdb-col>
      </mdb-col>
      <mdb-col class="find-board">
        <mdb-col class="centered">
          <h2 style="color:#ff033e">Find Padawan's Board</h2>

          <mdb-container>
            <mdb-row>
              <mdb-col style="margin: 2em;">
                <mdb-input
                  v-model="boardUUID"
                  label="Board Id"
                  type="Text"
                  size="sm"
                />
              </mdb-col>
              <mdb-col style="margin: 2em;">
                <mdb-input
                  v-on:keyup.native.enter="getBoard"
                  v-model="boardPassword"
                  label="Password"
                  type="password"
                  size="sm"
                />
              </mdb-col>
            </mdb-row>

            <mdb-btn gradient="blue" rounded v-on:click="getBoard">
              Find
            </mdb-btn>

            <mdb-row>
              <mdb-col style="margin: 2em;">
                <p>{{ board }}</p>
              </mdb-col>
            </mdb-row>
            <mdb-row>
              <mdb-col style="margin: 2em;">
                <p>{{ boardCountDown }}</p>
              </mdb-col>
            </mdb-row>
          </mdb-container>
        </mdb-col>
      </mdb-col></mdb-row
    >
  </mdb-container>
</template>

<script>
import Board from './Board'
import {
  mdbContainer,
  mdbRow,
  mdbCol,
  mdbCard,
  mdbCardBody,
  mdbInput,
  mdbBtn,
  mdbIcon
} from 'mdbvue'

export default {
  name: 'Index',
  components: {
    Board,
    mdbContainer,
    mdbRow,
    mdbCol,
    mdbCard,
    mdbCardBody,
    mdbInput,
    mdbBtn,
    mdbIcon
  },
  data() {
    return {
      board: '',
      boardCountDown: '',
      boardUUID: '',
      boardPassword: ''
    }
  },
  sockets: {
    getBoardResult(io) {
      this.board = io.data.board
      this.boardCountDown = io.data.boardCountDown
    },

    getBoardCountDown(io) {
      this.boardCountDown = io.data.boardCountDown
    }
  },
  methods: {
    getBoard() {
      this.$socket.emit('getBoard', {
        uuid: this.boardUUID,
        boardPassword: this.boardPassword
      })
    }
  }
}
</script>

<style scoped>
.centered {
  display: initial;
  vertical-align: middle;
  text-align: center;
}
.fill {
  height: 100%;
  width: 100%;
  padding: 0px !important;
  margin: 0px !important;
}

.padawan-board {
  background-color: #f2f2f2;
}

.find-board {
  background-color: #e6e6e6;
}
</style>
