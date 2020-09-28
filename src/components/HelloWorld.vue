<template>
  <div class="hello">
    <print></print>
    <h1>浏览器打印解决方案</h1>
    <h2>转换dom元素为图片，实现打印样式的统一。</h2>
    <h2>可设置浏览器打印画布大小，方向</h2>
   
  </div>
</template>

<script>
import print from './plugs/print.vue'
export default {
  name: 'HelloWorld',
  components: {print},
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
