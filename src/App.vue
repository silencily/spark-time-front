<template>
  <div id="app">
    <Header/>
    <div class="main">
      <div class="content">
        <el-row :gutter="20">
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-20*1000)" content="哈哈"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-5*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-30*1000)"/>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-20*1000)" content="哈哈"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-5*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-30*1000)"/>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-20*1000)" content="哈哈"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-5*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-30*1000)"/>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-20*1000)" content="哈哈"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-5*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-30*1000)"/>
          </el-col>
        </el-row>
        <el-row :gutter="20">
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-20*1000)" content="哈哈"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/3.jpg" :createdTime="new Date(new Date().getTime()-10*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-5*1000)"/>
          </el-col>
          <el-col :span="6">
            <spark imgPath="/static/img/2.jpg" :createdTime="new Date(new Date().getTime()-30*1000)"/>
          </el-col>
        </el-row>
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
  .content{
    margin: 0 50px;
    padding: 5px;
  }
</style>
