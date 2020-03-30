<template>
<div>
  <home-header class="main-header"></home-header>
  <scroller class="main-list" loadmoreoffset='300' offset-accuracy='300'>
    <div class="cell-btn">
      <home-image-slider></home-image-slider>
      <div class="slogen">
        <text class="i-slg iconfont">&#xe657; 网易自营品牌</text>
        <text class="i-slg iconfont">&#xe657; 30天无忧退货</text>
        <text class="i-slg iconfont">&#xe657; 48小时快速退款</text>
      </div>
    </div>
  </scroller>
  <home-nav class="main-nav"></home-nav>
  <text class="vuex-test-btn" @click="increase">Vuex测试</text>
  <text class="navigator-test-btn" @click="goto">Navigator测试</text>
  <text class="stream-test-btn" @click="fetch">Stream测试</text>
</div>
</template>

<script>
import HomeHeader from '@/components/HomeHeader'
import HomeNav from '@/components/HomeNav'
import HomeImageSlider from '@/components/HomeImageSlider'
// 导入navigator模块
const navigator = weex.requireModule('navigator')
const modal = weex.requireModule('modal')
const stream = weex.requireModule('stream') || {}
const apiUrl = 'https://jsonplaceholder.typicode.com/posts'

import store from '@/store'
export default {
  components: {
    HomeHeader,
    HomeNav,
    HomeImageSlider,
    
  },
  data() {
    return {
      isShowNav: false,
      title: 'article title',
      content: 'article content'
    }
  },
  methods: {
    increase() {
      // 提交vuex状态，调用actions中的方法
      store.dispatch('increase', true)
    },
    goto() {
      navigator.push(
        {
          // url: 'http://g.tbcdn.cn/amte-fe/amte-resource/0.0.8/fast/show_2.js',
          url: 'https://weex.apache.org/zh/docs/styles/common-styles.html#%E7%9B%92%E6%A8%A1%E5%9E%8B',
          animated: 'true'
        },
        event => {
          modal.toast({
            message: 'open a new weex page.',
            duration: 3
          })
        }
      )
    },
    fetch() {
      const { title, content } = this
      const body = JSON.stringify({ title, content })
      stream.fetch(
        {
          method: 'POST',
          url: apiUrl,
          type: 'json',
          body: body,
          headers: { custom: 'yezhongzheng' }
        },
        function(ret) {
          if (!ret.ok) {
            console.log(1)
            modal.toast({
              message: 'Network Error!',
              duration: 3
            })
          } else {
            console.log(2)
            modal.toast({
              message: '提交成功!' + body,
              duration: 3
            })
          }
        }
      )
    }
  }
}
</script>

<style lang="scss" scoped>
/* 导入scss文件，就可以使用其中声明的变量 */
@import '../assets/css/dimens.scss';
.vuex-test-btn {
  position: fixed;
  width: $testBtnWidth;
  height: 90px;
  top: 700px;
  left: 30px;
  background-color: red;
  color: white;
  border-radius: 30px;
  text-align: center;
  line-height: 90px;
}
.navigator-test-btn {
  position: fixed;
  width: 250px;
  height: 90px;
  top: 700px;
  left: 255px;
  background-color: red;
  color: white;
  border-radius: 30px;
  text-align: center;
  line-height: 90px;
}
.stream-test-btn {
  position: fixed;
  width: $testBtnWidth;
  height: 90px;
  top: 700px;
  left: 530px;
  background-color: red;
  color: white;
  border-radius: 30px;
  text-align: center;
  line-height: 90px;
}
.iconfont {
  font-family: myico;
}
.mian-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
}
.main-list {
  position: fixed;
  top: 159px;
  bottom: 90px;
  left: 0;
  right: 0;
}
.main-nav {
  margin-top: 10px;
}
.cell-btn {
  padding-bottom: 15px;
  /* margin-bottom: 20px; */
}
.slogen {
  flex-direction: row;
  justify-content: space-between;
  background-color: #ffffff;
}
.i-slg {
  flex: 1;
  height: 64px;
  padding-top: 16px;
  font-size: 24px;
  color: #ff0000;
  text-align: center;
}
</style>
