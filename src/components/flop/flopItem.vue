/*
 * @Author: maijc
 * @Date: 2019-08-04 11:50:31
 * @Last Modified by: maijc
 * @Last Modified time: 2019-08-04 17:41:48
 */

<!-- 翻牌元素组件 -->
<template>
  <div class="filp-item" :class="[size ? 'filp-item__'+size: '']">
    <div class="num-front">
      <div class="front-top">{{value}}</div>
      <div class="front-bottom">{{value}}</div>
    </div>
    <div class="num-under">
      <div :class="['under-bottom',{'active':active}]">
        <div class="under-content">{{value}}</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'flopItem',
  // 引入控件
  components: {},
  props: {
    size: {},
    value: {
      default: 0
    }
  },
  // 控件缓存数据
  data () {
    return {
      active: false,
      timer: undefined
    }
  },
  // 即时计算的属性
  computed: {},
  // 监控data中的数据变化
  watch: {
    // 检测数值是否有变化,有变化进行翻牌
    value (val, oldVal) {
      if (val === oldVal || val === ',' || val === '.') return
      this.active = false
      clearTimeout(this.timer)
      setTimeout(() => {
        this.active = true
        this.timer = setTimeout(() => {
          this.active = false
        }, 1100)
      })
    }
  },
  // 方法集合
  methods: {

  },
  // 生命周期 - 创建完成（可以访问当前this实例
  created () {

  },
  // 生命周期 - 挂载完成（可以访问DOM元素）
  mounted () {

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
  beforeDestroy () { },
  // 生命周期 - 销毁完成
  destroyed () { },
  // 如果页面有keep-alive缓存功能，这个函数会触发
  activated () { }
}
</script>
<style lang='scss' scoped>
.filp-item {
  position: relative;
  width: 17px;
  height: 38px;
  font-size: 20px;
  line-height: 37px;
  border: 1px solid rgba(48, 61, 118, 1);
  border-radius: 4px;
  overflow: hidden;
  + .filp-item {
    margin-left: 2px;
  }

  .num-front {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    text-align: center;
  }
  .num-front .front-top {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 50%;
    overflow: hidden;
    background: rgba(0, 0, 0, 1);
  }
  .num-front .front-bottom {
    position: absolute;
    left: 0;
    top: 50%;
    width: 100%;
    height: 50%;
    line-height: 0;
    overflow: hidden;
    background: rgba(0, 0, 0, 1);
  }

  .num-under {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    text-align: center;
  }

  .num-under .under-bottom {
    position: absolute;
    left: 0;
    top: 50%;
    width: 100%;
    height: 50%;
    overflow: hidden;
    transform-origin: center top;
  }
  // 下方显示数字
  .num-under .under-content {
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    line-height: 0;
    z-index: 99;
    background: rgba(0, 0, 0, 1);
  }
  // 动画
  @keyframes revolveScale {
    from {
      transform: rotateX(180deg);
      width: 100%;
    }
    to {
      transform: rotateX(0);
    }
  }
  .active {
    animation: revolveScale 1s;
    animation-direction: normal;
    animation-fill-mode: forwards;
  }
}
.filp-item__12-36 {
  width: 12px;
  height: 36px;
  font-size: 15px;
  line-height: 35px;
}
.filp-item__15-34 {
  width: 15px;
  height: 34px;
  font-size: 16px;
  line-height: 33px;
}
.filp-item__9-24 {
  width: 9px;
  height: 24px;
  font-size: 9px;
  line-height: 23px;
  + .filp-item {
    margin-left: 1px;
  }
}
</style>
