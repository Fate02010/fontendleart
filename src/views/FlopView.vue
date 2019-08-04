/*
 * @Author: maijc
 * @Date: 2019-08-04 12:28:59
 * @Last Modified by: maijc
 * @Last Modified time: 2019-08-04 17:45:05
 */

<!-- 翻牌 demo 界面 -->
<template>
  <div class="count-box">
    <flop class="count-item" size="15-34" align="left" :value="flopData"></flop>
  </div>
</template>

<script>
import flop from '../components/flop/index'
import { setInterval, clearInterval } from 'timers'
export default {
  // 引入控件
  components: {
    flop
  },
  // 控件缓存数据
  data () {
    return {
      timer: undefined,
      flopData: {
        title: '翻牌demo',
        data: '0',
        unit: '个'
      }
    }
  },
  // 即时计算的属性
  computed: {},
  // 监控data中的数据变化
  watch: {},
  // 方法集合
  methods: {

  },
  // 生命周期 - 创建完成（可以访问当前this实例
  created () {

  },
  // 生命周期 - 挂载完成（可以访问DOM元素）
  mounted () {
    let i = 0
    let self = this
    this.timer = setInterval(() => {
      self.flopData.data = i + ''
      i++
    }, 2000)
  },
  // 生命周期 - 创建之前
  beforeCreate () { },
  // 生命周期 - 挂载之前
  beforeMount () { },
  // 生命周期 - 更新之前
  beforeUpdate () { },
  // 生命周期 - 更新之后
  updated () { },
  // 生命周期 - 销毁之前
  beforeDestroy () {
    clearInterval(this.timer)
  },
  // 生命周期 - 销毁完成
  destroyed () { },
  // 如果页面有keep-alive缓存功能，这个函数会触发
  activated () { }
}
</script>
<style lang='scss' scoped>
.count-box {
  position: absolute;
  top: 30px;
  left: 0;
  right: 700px;
  width: 154px;
}
.count-item {
  padding: 10px 8px;
  border: 1px solid rgba(74, 137, 241, 1);
  + .count-item {
    margin-top: 23px;
  }
}
</style>
