<template>
  <div class="app-footer">
    <div class="footer-container">
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="copy-right">
            <span>© 2018 Silencily</span>
            <span>Power by <a href="https://www.vuejs.org" target="_blank">vuejs.org</a> && <a
              href="https://www.iris-go.com" target="_blank">iris-go.com</a></span>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="publish">
            <el-button type="primary" icon="el-icon-circle-plus-outline" circle></el-button>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="about">
            <a href="#" @click="showAbout"><img class="avatar avatar-42" src="/static/img/avatar-195x195.png" width="42"
                                                height="42"
                                                alt=""></a>
            <p>About Silencily</p>
          </div>
        </el-col>
      </el-row>
    </div>
    <el-dialog
      title="关于 Silencily"
      :modal="false"
      :visible.sync="aboutShown"
      width="60%"
      top="18vh"
      :close-on-click-modal="false"
      center>
      <div class="about-dialog-content">
        <el-carousel :interval="4000" type="card" height="200px">
          <el-carousel-item lable="person">
            <img src="/static/img/avatar-195x195.png"/>
            <h3>Silencily | A Person</h3>
          </el-carousel-item>
          <el-carousel-item lable="programmer">
            <img src="/static/img/avatar-195x195.png"/>
            <h3>Silencily | A Programmer</h3>
          </el-carousel-item>
          <el-carousel-item lable="father">
            <img src="/static/img/avatar-195x195.png"/>
            <h3>Silencily | A Father</h3>
          </el-carousel-item>
        </el-carousel>
        <div class="about-contacts">
          <div class="about-contacts-email">
            <a href="mailto:silencily@126.com"><i class="fa fa-envelope"></i>：silencily@126.com</a>
          </div>
          <div>
            <ul>
              <li>
                <a href="https://github.com/silencily" target="_blank"><i class="fa fa-github"
                                                                          aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-facebook" aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-twitter" aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-google-plus" aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="#"><i class="fa fa-linkedin" aria-hidden="true"></i></a>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </el-dialog>

  </div>
</template>

<script>
  export default {
    name: 'Footer',
    data (){
      return {
        aboutShown: false
      }
    },
    methods: {
      showAbout: function () {
        this.aboutShown = true
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .app-footer {
    width: 100%;
    position: fixed;
    bottom: 0;
    left: 0;
    background: rgba(0, 0, 0, 0.5);
  }

  .footer-container {
    margin: auto 50px;
    padding: 10px 0;
  }

  .copy-right {
    vertical-align: middle;
    color: #ffffff;
  }

  .copy-right span {
    display: block;
    padding: 5px 0;
  }

  .copy-right span a {
    color: #ffffff;
  }

  .publish {
    text-align: center;
  }

  .publish button {
    font-size: 35px;
  }

  .about {
    float: right;
    text-align: center;
  }

  .about p {
    margin: 0;
    font-size: 12px;
    color: #ffffff;
  }

  .avatar {
    border-radius: 50%;
  }

  .avatar-42 {
    width: 42px;
    height: 42px;
  }

  .el-carousel__item {
    text-align: center;
    background-color: #d3dce6;
  }

  .el-carousel__item h3 {
    color: #ffffff;
    font-size: 14px;
    opacity: 0.75;
    margin: 0;
    text-align: center;
    position: absolute;
    bottom: 0;
    width: 100%;
    background: #000000;
    font-weight: normal;
  }

  .about-contacts {
    text-align: center;
    font-size: 16px;
  }

  .about-contacts-email a {
    text-decoration: none;
    color: #000000;
  }

  .about-contacts ul {
    list-style: disc;
    padding: 0;
  }

  .about-contacts ul li {
    list-style: none;
    display: inline;
    margin-right: 5px;
  }

  .about-contacts ul li a {
    display: inline-block;
    font-size: 18px;
    line-height: 38px;
    color: #252525;
    height: 36px;
    width: 36px;
    background-color: rgba(0, 0, 0, .5);
    border-radius: 100%;
    text-align: center;
    -webkit-transition: .25s;
    transition: .25s;
  }

  .about-contacts ul li a:hover {
    background-color: #FB383B;
    color: #fff;
  }

</style>
