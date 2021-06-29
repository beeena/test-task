<template>
  <div id="app">
    <Tasks/>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Tasks from "./components/Tasks.vue";

@Component({
  components: {
    Tasks,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 60px;
}
</style>
