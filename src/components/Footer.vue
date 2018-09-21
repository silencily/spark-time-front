<template>
  <div class="app-footer">
    <div class="footer-container">
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="copy-right">
            <span>© 2018 Silencily</span>
            <span>Power by <a href="https://www.vuejs.org" target="_blank">vuejs.org</a> && <a href="https://www.iris-go.com" target="_blank">iris-go.com</a></span>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="publish">
            <el-button type="primary" icon="el-icon-circle-plus-outline" circle></el-button>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="about">
            <a href="#"><img class="avatar avatar-42" src="/static/img/avatar-195x195.png" width="42" height="42" alt=""></a>
            <p>About Silencily</p>
          </div>
        </el-col>
      </el-row>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Footer'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .app-footer{
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
  }
  .footer-container{
    margin: auto 50px;
    padding: 10px 0;
  }
  .copy-right{
    vertical-align:middle;
    color: #ffffff;
  }
  .copy-right span{
    display: block;
    padding: 5px 0;
  }
  .copy-right span a{
    color: #ffffff;
  }
  .publish{
    text-align: center;
  }
  .publish button{
    font-size: 35px;
  }
  .about{
    float: right;
    text-align: center;
  }
  .about p{
    margin: 0;
    font-size: 12px;
    color: #ffffff;
  }
  .avatar{
    border-radius: 50%;
  }
  .avatar-42{
    width: 42px;
    height: 42px;
  }

</style>
