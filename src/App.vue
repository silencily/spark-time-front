<template>
  <div id="app">
    <Header/>
    <div class="main">

    </div>
    <Footer/>
  </div>
</template>

<script>
import Header from './components/Header'
import Footer from './components/Footer'

export default {
  name: 'App',
  components: {
    Header,
    Footer
  }
}
</script>

<style>
  #app {
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;

  }

  .main {
    background: #333333;
    min-height: 800px;
    margin-top: 100px;
  }
</style>
