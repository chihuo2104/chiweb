<template>
  <div id="copyright" :class="{'hidden':this.$store.state.isCopyrightHidden}">
    Powered by <a href="//im.chihuo2104.dev" target="_blank">chihuo2104</a>.
    All rights reserved &copy;2018-{{new Date().getFullYear()}}.
    <br>
    <a href="//github.com/chihuo2104/chiweb/" target="_blank">Chiweb</a> Application Version:V3.3(Moe).
    Package Date:2021-12-31.
    <br>
    Engined by <a href="//cn.vuejs.org" target="blank">Vue</a>&amp;
    <a href="//nodejs.org" target="blank">Node.js</a>&amp;
    <a href="//webpack.js.org" target="blank">Webpack</a>&amp;
    <a target="_blank" href="//jenkins.io">Jenkins</a>.
    <a href="//icp.gov.moe/?keyword=20212104" target="_blank">{{$t('moenum')}}</a>
    <br>{{$t('showalive')}}{{aliveshow}}&nbsp;Thanks to <a href="//raycoder.me" target="blank">Ray</a>!<br>
    {{$t('statement1')}}<a href="//hypergryph.com" target="_blank">{{$t('hy')}}</a>{{$t('and')}}<a href="//www.mihoyo.com" target="_blank">{{$t('mhy')}}</a>{{$t('statement2')}}
  </div>
</template>
<script>
export default {
  data () {
    return {
      alive: {
        day: 0,
        hour: 0,
        min: 0,
        sec: 0
      },
      starttime: 1632110400
    }
  },
  mounted () {
    this.timer = setInterval(() => {
      const now = parseInt(Math.round(new Date() / 1000))
      this.alive = {
        day: this.tozero(parseInt((now - this.starttime) / (60 * 60 * 24))),
        hour: this.tozero(parseInt((now - this.starttime) % (60 * 60 * 24) / (60 * 60))),
        min: this.tozero(parseInt((now - this.starttime) % (60 * 60 * 24) % (60 * 60) / 60)),
        sec: this.tozero(parseInt((now - this.starttime) % (60 * 60 * 24) % (60 * 60) % 60))
      }
    }, 1000)
  },
  destoryed () {
    clearInterval(this.timer)
  },
  computed: {
    aliveshow: {
      get () {
        return this.$t('times', { day: this.alive.day, hour: this.alive.hour, min: this.alive.min, sec: this.alive.sec })
      }
    }
  },
  methods: {
    tozero (num) {
      return (num < 10) ? '0' + num : num
    }
  }
}
</script>
<style lang="less" scoped>
// vars
@import "../style/importme.less";
#copyright {
  background-color: rgba(255, 255, 255, 0.45);
  backdrop-filter: blur(15px);
  text-align: center;
  padding: 10px;
  font-size: @basicfont;
  width: 100%;
  bottom: 0;
  left:0;
  right:0;
  transition:bottom 2s ease-in-out;
  position: fixed;
  z-index: 12345;
}
.hidden{
  bottom: calc(0px - 40%) !important;
}
</style>
