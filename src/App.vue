<template>
  <div id="app">
    <router-view />
    <notifications
      group="boardSaved"
      position="bottom center"
      :max="3"
      :width="400"
    />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>

<style>
html,
body,
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #555555;
  height: 100%;
  width: 100%;
}
</style>
