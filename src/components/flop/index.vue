/*
 * @Author: maijc
 * @Date: 2019-08-04 11:57:53
 * @Last Modified by: maijc
 * @Last Modified time: 2019-08-04 17:43:35
 */

<!-- 翻牌组件 -->
<template>
  <div
    class="filp-box"
    :class="[align ? 'filp-box__'+align: '',alignItem ? 'filp-box-item__'+alignItem : '',size ? 'filp-box__'+size: '']"
  >
    <div class="item-title" v-if="value.title">
      <i class="iconfont" v-if="value.titleIcon" :class="value.titleIcon"></i>
      {{value.title}}
    </div>
    <div class="item-body">
      <i class="iconfont" v-if="value.icon" :class="value.icon"></i>
      <div class="item-num">
        <flop-item v-for="(item,index) in filpArr" :key="index" :value="item" :size="size"></flop-item>
        <div class="unit" v-if="value.unit">{{value.unit}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import flopItem from './flopItem'
export default {
  // 引入控件
  components: {
    flopItem
  },
  props: {
    size: {},
    value: {
      default () {
        return {
          data: '0000'
        }
      }
    },
    align: {},
    alignItem: {}
  },
  // 控件缓存数据
  data () {
    return {
      frontClass: false
    }
  },
  // 即时计算的属性
  computed: {
    filpArr () {
      return this.thousands(this.value.data)
    }
  },
  // 监控data中的数据变化
  watch: {},
  // 方法集合
  methods: {
    /**
    * 千分位计算
    * @method thousands
    * @param {string} val 传入的值
    * @return {array} 返回千分位arr数组
    */
    thousands (val) {
      var str = val + ''
      var value = str.split('.')
      let num = value[0].split('').reverse().reduce((prev, next, index) => {
        return ((index % 3) ? next : (next + ',')) + prev
      })
      let arrVal = value[1] ? num + '.' + value[1] : num
      let arr = arrVal.split('')
      return arr
    }
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
.filp-box {
  display: flex;
  flex-direction: column;
  min-width: 0;
  align-items: center;
  justify-content: center;
  font-size: 10px;
  color: #fff;
  .item-title {
    display: flex;
    align-items: center;
    line-height: 1;
    margin-bottom: 7px;
    .iconfont {
      margin-right: 6px;
      font-size: 12px;
    }
  }
  .item-body {
    display: flex;
    align-items: center;
    line-height: 1;
    width: 100%;
    .iconfont {
      font-size: 30px;
      margin-right: 9px;
    }
  }
  .item-num {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: flex-end;
    position: relative;
  }
  .unit {
    margin-left: 5px;
  }
}
.filp-box__left {
  align-items: flex-start;
}
.filp-box__right {
  align-items: flex-end;
}
.filp-box-item__left {
  .item-num {
    justify-content: flex-start;
  }
}
.filp-box__12-36 {
  .unit {
    margin-left: 4px;
  }
}
.filp-box__15-34 {
  .item-body {
    .iconfont {
      font-size: 25px;
    }
  }
  .unit {
    margin-left: 3px;
  }
}

.filp-box__9-24 {
  font-size: 6px;
  .item-title {
    margin-bottom: 4px;
  }
  .unit {
    margin-left: 3px;
  }
}
</style>
