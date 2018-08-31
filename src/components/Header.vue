<template>
  <div class="app-header">
    <div class="nav">
      <a class="logo" href="/">
        <img v-bind:src="logo">
      </a>
    </div>
  </div>
</template>

<script>
  let logoPath = require('../assets/logo.png')
  let logoPathW = require('../assets/logo-w.png')
  export default {
    name: 'Header',
    data(){
      return {
        logo: logoPath
      }
    },
    mounted: function () {
      this.$nextTick(function () {
        window.addEventListener('scroll', this.onScroll)
      })
    },
    methods: {
      onScroll () {
        let scrolled = document.documentElement.scrollTop || document.body.scrollTop
        if (scrolled >= 100) {
          this.logo = logoPathW
        } else {
          this.logo = logoPath
        }
      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .logo {
    display: inline-block;
    height: 100%;
  }

  .logo img {
    height: 100%;
  }

  .app-header {
    position: fixed;
    width: 100%;
    left: 0;
    top: 0;
    text-align: center;
    background: rgba(0, 0, 0, 0.6) none repeat scroll 0 0;
    box-shadow: 0 1px 3px rgba(50, 50, 50, 0.4);
  }

  .app-header:after {
    content: '';
    display: block;
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background: url(/static/img/bs-pattern.png) repeat center center;
    opacity: .4;
    z-index: -1;
  }

  .nav {
    font-size: 0;
    height: 100px;
  }
</style>
