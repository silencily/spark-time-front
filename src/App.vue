<template>
  <div id="app">
    <Header/>
    <div class="main">
      <div class="waterfall">
        <spark v-for="(value,key,index) in sparkContainer" class="waterfall-item" :img-name="value.img_name"
               :created-time="value.created_time" :content="value.content" :key="index" :id="key"
               @sparkDestroyed="handleSparkDestroyed"/>
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
    data() {
      return {
        sparkContainer: {},
        loadTimer: null
      }
    },
    components: {
      Header,
      Footer,
      spark
    },
    methods: {
      loadData(){
        this.axios.get('./spark')
          .then(res => {
            for (let spark in res.data) {
              this.$set(this.sparkContainer, spark._id, spark)
            }
          })
      },
      handleSparkDestroyed(id){
        console.log('the destroyed spark id in sparks: ' + id)
        delete this.sparkContainer[id]
        console.log(this.sparkContainer)
      },
      buildLoadTimer(){
        this.loadTimer = setInterval(() => {
          this.loadData()
        }, 35 * 1000)
      }
    },
    created(){
      this.loadData()
    },
    mounted: function () {
      this.buildLoadTimer()
    },
    destroyed: function () {
      clearInterval(this.loadTimer)
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

  .waterfall-item {
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
