<template>
  <mdb-container>
    <mdb-row>
      <mdb-col style="margin: 2em;">
        <mdb-input v-model="board" label="Board" type="textarea" size="sm" />
      </mdb-col>
    </mdb-row>
    <mdb-row>
      <mdb-col>
        <mdb-input
          v-model="boardTime"
          label="Time"
          type="number"
          min="1"
          size="sm"
        />
      </mdb-col>
      <mdb-col>
        <mdb-input
          v-on:keyup.native.enter="saveBoard"
          v-model="boardPassword"
          label="Password"
          type="password"
          size="sm"
        />
      </mdb-col>
    </mdb-row>
    <mdb-btn gradient="green" rounded v-on:click="saveBoard">
      Save
    </mdb-btn>
    <div>
      <br />
      <br />
      <p>id : {{ boardUUID }}</p>
      <p>time : {{ boardCountDown }}</p>
    </div>
  </mdb-container>
</template>

<script>
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
  name: 'Board',
  components: {
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
      boardTime: 60,
      boardPassword: '',
      boardUUID: '',
      boardCountDown: ''
    }
  },
  sockets: {
    boardCountDown(io) {
      this.boardCountDown = io.data.boardCountDown
    },
    boardSaved(io) {
      this.$notify({
        group: 'boardSaved',
        title: 'Board Saved!',
        text: io.data.uuid,
        type: 'success'
      })
      this.boardUUID = io.data.uuid
      this.boardCountDown = io.data.boardCountDown
    }
  },
  methods: {
    saveBoard() {
      this.$socket.emit('saveBoard', {
        board: this.board,
        boardTime: this.boardTime,
        boardPassword: this.boardPassword
      })
    }
  }
}
</script>
