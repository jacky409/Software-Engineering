<template >

 <vue-waterfall-easy :imgsArr="imgsArr" @scrollReachBottom="getData">

  <div slot = "waterfall-head" ><van-nav-bar    style="color:white" >
  <van-icon name="add-o" size="30" slot="left"/>
  <van-icon name="chat-o" size="25" slot="right"/>

</van-nav-bar>
<van-row type="flex" gutter="0" justify="space-around">
<van-col span="6">  <div style = "border-radius:140px;"><van-image  style = "border-radius:40px;" src="./../static/img2/18.jpg"></van-image></div></van-col> 
<van-col span="6"> <div style = "border-radius:50px;"><van-image    style = "border-radius:40px;" src="./../static/img2/17.jpg"></van-image></div></van-col>

<van-col span="6">  <div style = "border-radius:140px;"><van-image  style = "border-radius:40px;" src="./../static/img2/19.jpg"></van-image></div></van-col>
<van-col span="4"> <div style = "border-radius:50px;"><van-image    style = "border-radius:40px;" src="./../static/img2/20.jpg"></van-image></div></van-col>
</van-row>

<van-row gutter="20">
  <van-col span="8"><div style="color:white"><b><big>&nbsp;&nbsp;Explore</big></b></div></van-col>
  <van-col span="8" ><div> <input type="text" style="float:left;color:white;background-color:white;border-radius:15px;width:200px;height:25px"/></div></van-col>
</van-row>
<br/>
<div style="color:white"><b>&nbsp;&nbsp;Recommended societies for you</b></div>
<van-row type="flex" gutter="2" justify="space-around">
<van-col span="5">  <van-image  style = "border-radius:40px;" src="./../static/img2/13.jpg"></van-image></van-col> 
<van-col span="5"> <van-image    style = "border-radius:40px;" src="./../static/img2/14.jpg"></van-image></van-col>

<van-col span="5">  <van-image  style = "border-radius:40px;" src="./../static/img2/16.jpg"></van-image></van-col>
<van-col span="5"> <van-image    style = "border-radius:40px;" src="./../static/img2/15.jpg"></van-image></van-col>
</van-row>
<div style="color:white"><b><big>&nbsp;&nbsp;Discover</big></b></div>
</div>
</vue-waterfall-easy>

</template>

<script> 
import vueWaterfallEasy from './vue-waterfall-easy/vue-waterfall-easy.vue'
import axios from 'axios'
import Alink from './vue-waterfall-easy/components/alink.vue'
export default {
  name: 'app',
  data() {
    return {
      imgsArr: [],
      group: 0, 
      pullDownDistance: 0
    }
  },
  components: {
    vueWaterfallEasy,
    Alink
  },
  methods: {
    getData() {
      axios.get('./static/mock/data.json?group=' + this.group) 
        .then(res => {
          this.group++
          if (this.group === 10) { 
            this.$refs.waterfall.waterfallOver()
            return
          }
          this.imgsArr = this.imgsArr.concat(res.data)
        })
    },
    clickFn(event, { index, value }) {
      if (event.target.tagName.toLowerCase() == 'img') {
        console.log('img clicked', index, value)
      }
    },
    imgErrorFn(imgItem){
      console.log('Error',imgItem)
    },
    changeImgArr() {
      axios.get('./static/mock/data-change.json') 
        .then(res => {
          this.imgsArr = res.data
        })
    },
    pullDownMove(pullDownDistance) {
      
      this.pullDownDistance = pullDownDistance
    },
    pullDownEnd(pullDownDistance) {
      console.log('pullDownEnd')
      if(this.pullDownDistance>50){
        alert('Push Down')
      }
      this.pullDownDistance = 0
    },
  },
  created() {
    this.getData()

    // setTimeout(()=>{
    //   this.imgsArr.splice(1,1)
    // },2000)
  },
}

</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  background-color: #10101a;
}

a {
  color: #000;
  text-decoration: none;
  &:active {
    color: #000;
  }
}
html,
body,
#app {
  height: 100%;
}

#app {
  position: relative;
  #header {
    display: block;
    text-align: center;
    background: #10101a;
    color: #10101a;
    line-height: 32px;
    font-size: 16px;
    font-weight: bold;
    letter-spacing: 2px;
    position: fixed;
    z-index: 999;
    width: 100%;
  }
  #content {
    position: absolute;
    top: 32px;
    bottom: 0;
    width: 100%;
  }
}
// .__err__ .img-wraper {
//   background: url(/static/img/1.jpg) no-repeat center/100px 100px !important;
// }
#app {
  overflow: auto;
  position: relative;
  .some-info {
    line-height: 1.6;
    text-align: center;
  }
}
</style>
