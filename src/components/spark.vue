<template>
  <div>
    <transition enter-active-class="jackInTheBox" leave-active-class="flash">
      <el-card :body-style="{ padding: '0px',position: 'relative'}" shadow="hover" class="animated">
        <img :src="'./spark/img/' + id" class="image" @click="showDetail" :alt="imgName">
        <div class="spark-content" v-show="content != null" @click="showDetail">
          <div class="spark-content-inner">{{content}}</div>
        </div>
        <div class="spark-time">
          <span v-if="isAd" style="color: #6f7180;">广告-燃尽(秒)：<span :class="{'time-red':timeRed}">{{lifetime}}</span></span>
          <span v-else>燃尽(秒)：<span :class="{'time-red':timeRed}">{{lifetime}}</span></span>
        </div>
      </el-card>
    </transition>
    <el-dialog
      :visible.sync="detailShown"
      top="16vh"
      custom-class="spark-dialog"
      :close-on-click-modal="false"
      center>
      <div class="spark-dialog-content">
        <img :src="'./spark/img/' + id" style="max-width: 100%">
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
      imgName: {
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
      },
      isAd: {
        type: Boolean
      }
    },
    data(){
      return {
        lifetime: 60,  //默认六十秒
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
      if (this.lifetime <= 3 && !this.timeRed) {
        this.timeRed = true
      }
      if (this.lifetime <= 0) {
        this.lifetime = 0
      }
      var timer = setInterval(() => {
        this.lifetime--
        if (this.lifetime <= 3 && !this.timeRed) {
          this.timeRed = true
        }
        if (this.lifetime <= 0) {
          this.lifetime = 0
          this.$emit('sparkDestroyed', this.id) //触发销毁事件
        }
      }, 1000)
      this.$once('hook:beforeDestroy', function () {
        clearInterval(timer)
      })
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
<style>
  .spark-dialog {
    width: 50% !important;
  }

  @media screen and (max-width: 768px) {
    .spark-dialog {
      width: 100% !important;
    }
  }
</style>
