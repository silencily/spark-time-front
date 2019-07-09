<template>
  <div class="app-footer">
    <div class="footer-container">
      <el-row :gutter="20">
        <el-col :span="8">
          <div class="copy-right">
            <span class="copy-right-author">© 2019 Silencily</span>
            <span class="copy-right-power">Power by <a href="https://www.vuejs.org" target="_blank">vuejs.org</a> && <a
              href="https://www.iris-go.com" target="_blank">iris-go.com</a></span>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="publish">
            <el-button type="primary" icon="el-icon-circle-plus-outline" circle @click="showPublish"></el-button>
          </div>
        </el-col>
        <el-col :span="8">
          <div class="about">
            <a href="#" @click="showAbout">
              <img class="avatar" src="/static/img/avatar.jpg"
                   alt="about silencily">
            </a>
            <p class="about-author-name">About Silencily</p>
          </div>
        </el-col>
      </el-row>
    </div>
    <el-dialog
      title="发布火花"
      :visible.sync="publishShown"
      top="16vh"
      :modal="false"
      custom-class="publish-dialog"
      :close-on-click-modal="false"
      center>
      <div class="publish-dialog-content">
        <el-row :gutter="10">
          <el-col :xs="7" :sm="7">
            <el-upload ref="publish"
                       class="publish-uploader"
                       name="sparkImage"
                       action="./spark"
                       :data="publishData"
                       :show-file-list="false"
                       :on-success="handlePublishSuccess"
                       :on-error="handlePublishError"
                       :on-change="handleImgAdded"
                       :before-upload="beforePublish" :accept="'image/jpeg,image/png'" :auto-upload="false">
              <img v-if="imageUrl" :src="imageUrl" class="publish-img">
              <i v-else class="el-icon-plus publish-uploader-icon"></i>
              <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
            </el-upload>
          </el-col>
          <el-col :xs="10" :sm="12">
            <el-input
              type="textarea"
              class="publish-text" v-model="sparkContent"
              maxlength="70"
              minlength="2"
              placeholder="发表火花文字（70字以内）">
            </el-input>
          </el-col>
          <el-col :xs="7" :sm="5">
            <div>
              <el-image :fit="'fill'" style="width:100%;height: 50px;cursor: pointer;" v-on:click="getCaptcha"
                        :src="captcha">
                <div slot="placeholder" class="image-slot">
                  加载中<span class="dot">...</span>
                </div>
                <div slot="error" class="image-slot" v-on:click="getCaptcha">
                  <i class="el-icon-picture-outline"></i>
                </div>
              </el-image>
            </div>
            <div style="color: #FB383B;font-size: 12px;text-align: center;">
              <span>点击图片更换验证码</span>
            </div>
            <div style="margin-top: 10px;">
              <el-input
                placeholder="验证码"
                clearable v-model="validCode">
              </el-input>
            </div>

          </el-col>
        </el-row>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="publishShown = false">取 消</el-button>
        <el-button type="primary" :loading="publishing" @click="publish">发 布</el-button>
      </span>
    </el-dialog>

    <el-dialog
      title="About Silencily"
      :modal="false"
      top="16vh"
      :visible.sync="aboutShown"
      custom-class="about-dialog"
      :close-on-click-modal="false"
      center>
      <div class="about-dialog-content">
        <el-carousel :interval="4000" type="card" height="200px">
          <el-carousel-item lable="person">
            <img src="/static/img/person.jpg" height="100%" width="100%"/>
            <h3>Silencily | A Person</h3>
          </el-carousel-item>
          <el-carousel-item lable="programmer">
            <img src="/static/img/programmer.png" height="100%" width="100%"/>
            <h3>Silencily | A Programmer</h3>
          </el-carousel-item>
          <el-carousel-item lable="father">
            <img src="/static/img/father.jpg" height="100%" width="100%"/>
            <h3>Silencily | A Father</h3>
          </el-carousel-item>
        </el-carousel>

        <div class="about-contacts">
          <div class="about-contacts-email">
            <a href="mailto:silencily@126.com"><i class="fa fa-envelope"></i>：silencily@126.com</a>
          </div>
          <div>
            <ul style="margin-bottom: 0px;">
              <li>
                <a href="https://github.com/silencily" target="_blank"><i class="fa fa-github"
                                                                          aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="https://www.facebook.com/seven.silencily" target="_blank"><i class="fa fa-facebook"
                                                                                      aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="https://twitter.com/silencily" target="_blank"><i class="fa fa-twitter" aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="https://plus.google.com/+silencilyseven" target="_blank"><i class="fa fa-google-plus"
                                                                                     aria-hidden="true"></i></a>
              </li>
              <li>
                <a href="https://www.linkedin.com/in/silencily-seven-915765175" target="_blank"><i
                  class="fa fa-linkedin" aria-hidden="true"></i></a>
              </li>
            </ul>
          </div>
          <div class="about-donating">
            <img src="/static/img/bitcoin.png"/>
            <span>Thanks for donating</span>
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
        aboutShown: false,
        publishShown: false,
        imageUrl: '',
        captcha: '',
        sparkContent: '',
        validCode: '',
        publishing: false
      }
    },
    computed: {
      publishData: {
        get: function () {
          return {"sparkContent": this.sparkContent, "validCode": this.validCode}
        },
        set: function () {
        }
      }
    },
    methods: {
      showAbout: function () {
        this.aboutShown = true
      },
      showPublish: function () {
        this.publishShown = true
        this.getCaptcha();
      },
      handlePublishSuccess(res, file) {
        let code = res.code
        let message = res.message
        if (code == "1") {
          this.$message.success(message);
          this.$refs.publish.clearFiles();
          this.sparkContent = ''
          this.validCode = ''
          this.publishShown = false
          this.publishing = false
          this.imageUrl = 'reset'
        } else {
          this.$message.error(message);
          this.publishing = false
          this.imageUrl = 'reset'
          this.getCaptcha();
        }

      },
      handlePublishError(err, file, fileList){
        this.$message.error('发布火花失败，请稍后重试！');
        this.publishing = false
        this.imageUrl = 'reset'
        this.getCaptcha();
      },
      beforePublish(file) {
        const isJPGPNG = file.type === 'image/jpeg' || file.type === 'image/png';
        const isLt500K = file.size / 1024 / 1024 < 0.5;

        if (!isJPGPNG) {
          this.$message.error('上传火花图片只能是 JPG/PNG 格式!');
          return false
        }
        if (!isLt500K) {
          this.$message.error('上传火花图片大小不能超过 500KB!');
          return false
        }
        return true;
      },
      handleImgAdded(file, fileList){
        if (this.imageUrl === 'reset') {
          this.imageUrl = ''
        } else {
          this.imageUrl = URL.createObjectURL(file.raw);
        }
      },
      getCaptcha(){
        this.axios.get('./spark/captcha?v=' + new Date().getTime()).then(res => {
          this.captcha = res.data
        }).catch(err => {
          console.log(err)
          this.captcha = new Date().getTime() + ''
        })
      },
      publish(){
        if (this.imageUrl === '') {
          this.$message.error('请选择花火图片!');
          return false
        }
        if (this.sparkContent === '') {
          this.$message.error('请填写花火文字!');
          return false
        }
        if (this.validCode === '') {
          this.$message.error('请输入验证码!');
          return false
        }
        this.publishing = true

        this.$refs.publish.submit();
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

  .copy-right-author {
    display: block;
    padding: 5px 0;
  }
  .copy-right-power{
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
  .about-donating{
    position: absolute;
    right: 25px;
    bottom: 25px;
    border: 1px solid #000;
    padding: 2px;
  }
  .about-donating img{
    display: block;
    width: 70px;
    margin: 0px auto;
  }
  .about-donating span{
    font-size: 12px;
    color: #000;
  }

  .publish-uploader {
    text-align: center;
  }

  .publish-uploader-icon {
    font-size: 28px;
    color: #FB383B;
    width: 115px;
    height: 115px;
    line-height: 115px;
    text-align: center;
  }

  .publish-img {
    width: 115px;
    height: 115px;
    display: block;
  }

  .el-upload__tip {
    color: #FB383B;
  }
  @media screen and (max-width: 768px) {
    .copy-right-power{
      display: none;
    }
    .about-author-name{
      display: none;
    }
    .avatar{
      width: 50px;
      height: 50px;
    }
    .about-donating{
      position: inherit;
      margin-top: 5px;
    }
    .publish-uploader-icon{
      width: 60px;
      height: 60px;
      line-height: 60px;
    }
    .publish-img{
      width: 60px;
      height: 60px;
    }
  }
</style>
<style>
  .publish-uploader .el-upload {
    border: 1px dashed rgb(254, 195, 196);
    border-radius: 6px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
  }

  .publish-uploader .el-upload:hover {
    border-color: #FB383B;
  }

  .publish-text textarea {
    height: 160px;
  }
  .publish-dialog{
    width: 50%;
  }
  .about-dialog{
    width: 60%;
  }

  .image-slot {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    background: #f5f7fa;
    color: #909399;
    font-size: 14px;
  }

  @media screen and (max-width: 768px) {
    .publish-dialog{
      width: 100%;
      margin-top: 15vh;
    }
    .about-dialog{
      width: 100%;
      margin-top: 15vh;
    }
  }

</style>
