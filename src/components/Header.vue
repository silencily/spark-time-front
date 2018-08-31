<template>
  <div class="nav">
    <el-container>
      <el-main>
        <a class="logo" href="/">
          <img src="/static/img/logo-sparktime.png">
        </a>
      </el-main>
    </el-container>
  </div>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .logo{
    display: inline-block;
    z-index: auto;
  }
  .nav{
    position: fixed;
    width: 100%;
    left: 0;
    top: 0;
    text-align: center;
    background: -webkit-gradient(linear,left bottom,right top,color-stop(0,#020031),color-stop(100%,#6d3353));
    z-index: 1500;
  }

  .nav:after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: url(/static/img/bs-pattern.png) repeat center center;
    opacity: .4;
    z-index: 1400;
  }
</style>
