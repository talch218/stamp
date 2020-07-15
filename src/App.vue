<template>
  <div id="app">
    <Stamp :value="name" />
  </div>
</template>

<script>
import Stamp from './components/Stamp.vue';

export default {
  name: 'App',
  components: {
    Stamp
  },
  data: () =>({
    name: '姓 名'
  }),
  mounted: function () {
    if (window.location.search) {
      this.name = decodeURI(window.location.search.substr(1));
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
