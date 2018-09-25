<template>
  <div>
    <transition enter-active-class="jackInTheBox" leave-active-class="flash">
      <el-card :body-style="{ padding: '0px',position: 'relative'}" shadow="hover" class="animated">
        <img :src="imgPath" class="image" @click="showDetail">
        <div class="spark-content" v-show="content != null" @click="showDetail">
          <div class="spark-content-inner">{{content}}</div>
        </div>
        <div class="spark-time">
          <span>燃尽(秒)：<span :class="{'time-red':timeRed}">{{lifetime}}</span></span>
        </div>
      </el-card>
    </transition>
    <el-dialog
      :visible.sync="detailShown"
      top="10vh"
      width="50%"
      :close-on-click-modal="false"
      center>
      <div class="spark-dialog-content">
        <img :src="imgPath" style="max-width: 100%">
        <p>{{content}}</p>
      </div>
      <span slot="footer" class="dialog-footer">
       <el-button type="primary" @click="detailShown = false">关 闭</el-button>
      </span>
    </el-dialog>
  </div>
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
        type: [Date, String],
        required: true
      },
      content: {
        type: String
      },
      id: {
        type: String,
        required: true
      }
    },
    data(){
      return {
        lifetime: 60000,  //默认六十秒
        timeRed: false,
        detailShown: false
      }
    },
    methods: {
      showDetail: function (event) {
        this.detailShown = true
      }
    },
    computed: {},
    filters: {
      dateFormat: function (val, pattern = 'YYYY-MM-DD HH:mm:ss') {
        return moment(val).format(pattern)
      }
    },
    created: function () {

    },
    mounted: function () {
      let passed = moment().diff(moment(this.createdTime), 'seconds')
      console.log('spark-' + this._uid + ' passed time:' + passed)
      this.lifetime = this.lifetime - passed
      let int = setInterval(() => {
        this.lifetime--
        if (this.lifetime <= 3 && !this.timeRed) {
          this.timeRed = true
        }
        if (this.lifetime <= 0) {
          this.lifetime = 0
          clearInterval(int)
          this.$emit('sparkDestroyed', this.id) //触发销毁事件
        }
      }, 1000)
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .el-card {
    border: none;
  }

  .time-red {
    color: #FB383B;
    font-weight: bold;
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
    font-size: 16px;
    color: #ffffff;
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

  .spark-dialog-content {
    text-align: center;
    color: #000000;
  }

  .image {
    width: 100%;
    display: block;
    cursor: pointer;
  }
</style>
