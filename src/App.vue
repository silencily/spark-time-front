<template>
  <div id="app">
    <Header/>
    <div class="main">
      <div class="waterfall">
        <spark v-for="(value,key,index) in sparks" class="waterfall-item" :img-path="value.imgPath"
               :created-time="value.createdTime" :content="value.content" :key="index" :id="key"
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
        sparks: {},
        dataGroup: '',
        loadSwitch: true // 设置一个开关来避免重负请求数据
      }
    },
    components: {
      Header,
      Footer,
      spark
    },
    methods: {
      initData(){
        this.axios.get('./static/mock/data-init.json') // 真实环境中，后端会根据参数group返回新的图片数组，这里我用一个惊呆json文件模拟
          .then(res => {
            for (let key of Object.keys(res.data)) {
              this.$set(this.sparks, key, res.data[key])
            }
          })
      },
      loadData(){
        this.axios.get('./static/mock/data' + this.dataGroup + '.json')
          .then(res => {
            if (this.dataGroup == '') {
              this.dataGroup = '2'
            } else {
              this.dataGroup = ''
            }
            for (let key of Object.keys(res.data)) {
              this.$set(this.sparks, key, res.data[key])
            }
            this.loadSwitch = true
          })
      },
      onScroll(){
        let scrolled = document.documentElement.scrollHeight - document.documentElement.clientHeight - document.documentElement.scrollTop
        if (scrolled <= 10) {
          if (this.loadSwitch) {
            console.log("handle scroll event")
            this.loadSwitch = false
            this.loadData()
          }
        }
      },
      handleSparkDestroyed(id){
        console.log('the destroyed spark id in sparks: ' + id)
        delete this.sparks[id]
        console.log(this.sparks)
      }
    },
    created(){
      this.initData()
    },
    mounted: function () {
      this.$nextTick(function () {
        window.addEventListener('scroll', this.onScroll)
      })
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
