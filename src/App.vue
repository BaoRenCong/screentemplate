<template>
  <div id="app" class="screen" ref="screen">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  mounted () {
    // 调用setScale，并设置事件监听
    this.setScale();
    window.addEventListener("resize", this.setScale);
  },
  methods: {
    getScale () {
      // 计算屏幕可视高度和宽度与屏幕的宽高的比例
      // 为了内容能够在屏幕中完整的显示，取两者之间小的值
      // const width = window.screen.width
      // const height = window.screen.height
      let ww = window.innerWidth / 1920;
      let wh = window.innerHeight / 1080;
      return ww < wh ? ww : wh;
    },
    setScale () {
      let scale = this.getScale();
      this.$refs.screen.style.setProperty("--scale", scale);
    },
  },
  destroyed () {
    // 页面销毁时移除监听事件
    window.removeEventListener('resize', this.setScale)
  },
  components: {
    HelloWorld
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.screen {
  --scale: 1;
  width: 1920px;
  height: 1080px;
  background-size: 100% 100%;
  position: absolute;
  transform: scale(var(--scale)) translate(-50%, -50%);
  display: flex;
  flex-direction: column;
  transform-origin: 0 0;
  left: 50%;
  top: 50%;
}
</style>
