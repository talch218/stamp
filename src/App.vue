<template>
  <div id="app">
    <Stamp :value="name" />
    <h6>ちょっと便利な使い方</h6>
    <p>URLに名前を含めておくと初期値として表示されます。</p>
    <p>田中太郎さん ⇒ https://talch218.github.io/stamp/?田中 太郎</p>
    <p>この状態でお気に入りに登録しておくと毎回入力しなくていいので便利</p>
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
