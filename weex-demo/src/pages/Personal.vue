<template>
  <scroller>
    <div class="wrapper">
      <text class="vuexTest">vuex测试{{storeCount}}</text>
    </div>
  </scroller>
</template>

<script>
const modal = weex.requireModule('modal');
import store from '@/store'
export default {
  computed: {
    storeCount() {
      return store.state.count
    }
  }
};
</script>

<style scoped>
.wrapper {
  padding-bottom: 150px;
}

.vuexTest {
  height: 94px;
  background-color: #ffffff;
  font-size: 28px;
  text-align: center;
  line-height: 94px;
}
</style>
