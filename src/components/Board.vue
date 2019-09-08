<template>
  <div class="">
    <br />
    <br />
    <h3>Board Text :</h3>
    <div class="">
      <input v-model="board" type="text" name="" value="" />
    </div>
    <br />
    <h3>Board Time :</h3>
    <div class="">
      <input v-model="boardTime" type="number" name="" value="60" />
    </div>
    <br />
    <h3>Board Password :</h3>
    <div class="">
      <input v-model="boardPassword" type="password" name="" value="" />
    </div>
    <br />
    <div class="">
      <button type="button" name="button" v-on:click="saveBoard">Save</button>
    </div>
    <br />
    <div class="">uuid : {{ boardUUID }}</div>

    <br />

    <div>
      {{ boardCountDown }}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Board',
  data() {
    return {
      board: '',
      boardTime: '',
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
