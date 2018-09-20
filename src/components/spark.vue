<template>
  <transition enter-active-class="jackInTheBox" leave-active-class="flash">
    <el-card :body-style="{ padding: '0px',position: 'relative'}" shadow="hover" class="animated" v-if="show">
      <img :src="imgPath" class="image" @click="showDetail">
      <div class="spark-content" v-show="content != null" @click="showDetail">
        <div class="spark-content-inner">{{content}}</div>
      </div>
      <div class="spark-time">
        <span>燃尽(秒)：{{lifetime}}</span>
      </div>
    </el-card>
  </transition>
</template>

<script>
  import moment from 'moment'
  import animate from 'animate.css'
  export default {
    name: 'spark',
    props: {
      imgPath: {
        type: String,
        required: true
      },
      createdTime: {
        type: Date,
        required: true
      },
      content: {
        type: String
      }
    },
    data(){
      return {
        lifetime: 30,  //默认三十秒
        show: false
      }
    },
    methods: {
      showDetail: function (event) {
        alert("in showDetail")
      }
    },
    computed: {},
    filters: {
      dateFormat: function (val, pattern = 'YYYY-MM-DD HH:mm:ss') {
        return moment(val).format(pattern)
      }
    },
    created: function () {
      let passed = moment().diff(moment(this.createdTime), 'seconds')
      console.log('spark-' + this._uid + ' passed time:' + passed)
      this.lifetime = this.lifetime - passed
      let int = setInterval(() => {
        this.lifetime--
        if (this.lifetime <= 0) {
          this.lifetime = 0
          clearInterval(int)
          this.show = false
        }
      }, 1000)
    },
    mounted: function () {
      this.show = true
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .el-card{
    border: none;
  }
  .spark-content {
    position: absolute;
    top: 0px;
    bottom: 0px;
    width: 100%;
    text-align: center;
    color: #000000;
    vertical-align: middle;
    background: rgba(0, 0, 0, 0.3);
    cursor: pointer;
  }

  .spark-content-inner {
    padding: 10px;
    font-size: 18px;
  }

  .spark-time {
    position: absolute;
    bottom: 0px;
    text-align: center;
    font-size: 14px;
    color: #ffffff;
    width: 100%;
    background: rgba(0, 0, 0, 0.5);
    padding: 3px 0;
  }

  .image {
    width: 100%;
    display: block;
    cursor: pointer;
  }
</style>
