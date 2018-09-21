<template>
  <div id="app">
    <Header/>
    <div class="main">
      <div class="waterfall">
        <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-20*1000)" content="哈哈" class="waterfall-item"/>
        <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-5*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/5.jpg" :createdTime="new Date(new Date().getTime()-13*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-17*1000)" content="哈哈" class="waterfall-item"/>
        <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/5.jpg" :createdTime="new Date(new Date().getTime()-5*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-30*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-8*1000)" content="哈哈" class="waterfall-item"/>
        <spark imgPath="/static/img/5.jpg" :createdTime="new Date(new Date().getTime()-22*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/5.jpg" :createdTime="new Date(new Date().getTime()-5*1000)" class="waterfall-item"/>
        <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-26*1000)" class="waterfall-item"/>
      </div>
    </div>
    <Footer/>
  </div>
</template>

<script>
  import Header from './components/Header'
  import Footer from './components/Footer'
  import spark from './components/spark'
  export default {
    name: 'App',
    components: {
      Header,
      Footer,
      spark
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

  .waterfall {
    padding: 5px;
    width: 80%;
    column-gap: 10px;
    column-count: 4;
    margin: 0 auto;
  }

  .waterfall-item{
    break-inside: avoid;
    margin-bottom: 10px;
  }

  @media (min-width: 992px) and (max-width: 1300px) {
    .waterfall {
      column-count: 3;
    }
  }

  @media (min-width: 768px) and (max-width: 991px) {
    .waterfall {
      column-count: 2;
    }
  }

  @media (max-width: 767px) {
    .waterfall {
      column-count: 1;
    }
  }
</style>
