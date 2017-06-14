<template>
  <div>
    <div :class='rulerstyle' :style="numeralsStyle">
      <div v-for="cm in length" class='cm' :style="cmstyle(cm)">
        <div v-for="mm in 9" class='mm' :style="mmstyle(mm)"></div>
      </div>
      <div class='cm' :style="cmstyle(length + 1)"></div>
    </div>
  </div>
</template>
<script >
export default {
  props: {
    mode: { // 刻度尺类型
      type: String,
      default: 'horizontal'
    },
    range: {// 刻度尺长度
      type: Number,
      default: 10
    },
    numeralsStyle: {// 刻度尺数字样式
      type: Object,
      default: () => {
        return {color: '#BBBBBB', 'font-size': '13px'}
      }
    },
    markColor: {// 刻度尺颜色
      type: String,
      default: 'black'
    }
  },
  computed: {
    length () {
      return Math.ceil(this.range / 10)
    },
    rulerstyle () {
      return this.mode === 'horizontal' ? 'ruler_h' : 'ruler_v'
    }
  },
  methods: {
    cmstyle (value) {
      switch (this.mode) {
        case 'vertical':
          return {top: `${value - 1}cm`, position: 'absolute', 'border-top': `1px solid ${this.markColor}`, width: '10px', height: '1cm'}
        default:
          return {left: `${value - 1}cm`, position: 'absolute', 'border-left': `1px solid ${this.markColor}`, height: '10px', width: '1cm'}
      }
    },
    mmstyle (value) {
      switch (this.mode) {
        case 'vertical':
          return {top: `${value}mm`, 'border-top': `1px solid ${this.markColor}`, position: 'absolute', width: '3px', height: '1mm', left: '7px'}
        default:
          return {left: `${value}mm`, 'border-left': `1px solid ${this.markColor}`, position: 'absolute', height: '3px', width: '1mm', top: '7px'}
      }
    }
  }
}

</script>
<style>
.ruler_h {
 position: relative;
 height: 12px;
 counter-reset: cmindex -1;
}
.ruler_v {
 position: relative;
 width: 12px;
 counter-reset: cmindex -1;
}

.ruler_h .cm:after {
 position: absolute;
 right: 9mm;
 bottom: 10px;
 content: counter(cmindex);
 counter-increment: cmindex;
}

.ruler_v .cm:after {
 position: absolute;
 right: 12px;
 top: -7px;
 content: counter(cmindex);
 counter-increment: cmindex;
}
</style>
