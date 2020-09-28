/* 测试打印
 * @Author: xuecs 
 */
<template>
  <div>
    <div id="printMe" ref="printContent">
      <ul class="content">
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
        <li>轻轻的我走来了，</li>
      </ul>
    </div>
    
    <button type="primary" @click="toImg(1)">打印（11in * 9.5in）</button>
    <button type="primary" @click="toImg(2)">打印（279pt * 241pt）</button>
    <button type="primary" @click="toImg(3)">横向打印</button>
    <button type="primary" @click="toImg(4)">纵向打印</button>
    <!--<el-button v-print="printObj" type="primary">直接打印</el-button>-->
    <img style="margin-top:20px;" :src="img" alt="">
    
  </div>
</template>

<script>
import html2canvas from 'html2canvas'  // 转图片打印需要先安装html2Canvas和print-js
import printJS from 'print-js'
export default {
  data () {
    return {
      img: '',
      printObj: {
        id: 'printMe',
        popTitle: '打印',
        extraCss: 'https://www.google.com,https://www.google.com',
        extraHead: '<meta http-equiv="Content-Language"content="zh-cn"/>'
      }
    }
  },
  methods: {
    toImg (type) { // 转图片打印
      html2canvas(this.$refs.printContent, {
        backgroundColor: null,
        useCORS: true,
        // windowHeight: document.body.scrollHeight,
        height:279,
        width: 241,
      }).then((canvas) => {
        const url = canvas.toDataURL()
        this.img = url
        var _pageStyle;
        switch(type){
          case 1:_pageStyle='@page {size:11in 9.5in ;}'; break;
          case 2:_pageStyle='@page {size:279pt 241pt ;}'; break;
          case 3:_pageStyle='@page {size: landscape;}'; break;
          case 4:_pageStyle='@page {size: portrait;}'; break;
        }

        printJS({
          printable: url,
          // maxWidth:241,
          type: 'image',
          documentTitle: '打印图片',
          // style: '@page {size: landscape;}'// 横（即，框的最长边是水平的）
          // style: '@page {size: portrait;}'// 竖（即，盒子的最长边是垂直的）
          // style: '@page {size:279pt 241pt ;}'//指定大小  
          style: _pageStyle//指定大小-英尺

          //复写纸规格：
          //1：全页（9.5英尺X11英尺，241mmX279mm）。2：二分一（9.5英尺X11/2英尺）。3：三分一（9.5英尺X11/3英尺）。

          //门店打印（1.0与易石）
          //打印方式有2种：
          //1.沿易撕线区分的固定尺寸(如9.5英尺X11/2英尺)每一页 有固定的页头信息和页尾签字合计信息，中间展示操作的物料信息。需要明确纸张的高度 拼接出打印内容。
          //2.自上向下打印，无论打印多少页，一次打印只有1个页头和一个页尾。（前端实现 选择物料打印功能 可以打印出 方式1的单据）

        })
      })
    }
  }
}
</script>
<style>
#printMe{
  
}
.content{
  float: left;
}
  #printMe li{
      list-style: none;
  }
</style>

