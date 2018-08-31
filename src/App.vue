<template>
  <div id="app">
    <Header/>
    <div class="main">

    </div>

  </div>
</template>

<script>
import Header from './components/Header.vue'

export default {
  name: 'App',
  components: {
    Header
  }
}
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

}
  .main{
    background: #333333;
    min-height: 800px;
    margin-top: 100px;
  }
</style>
