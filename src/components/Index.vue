<template>
  <div class="">
    <Board />

    <h5>**************************************</h5>

    <h4>Board UUID</h4>
    <input v-model="boardUUID" type="text" name="" value="" />
    <h4>Board Password</h4>
    <input v-model="boardPassword" type="password" name="" value="" />
    <button type="button" name="button" v-on:click="getBoard">Find</button>

    <h4>Board :</h4>

    <div class="">
      <h2>-----------------------------</h2>
      {{ board }}
      <h2>-----------------------------</h2>
    </div>

    <br />
    <br />

    <div class="">
      {{ boardCountDown }}
    </div>
  </div>
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
