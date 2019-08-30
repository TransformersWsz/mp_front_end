<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import resize from './resize'

const animationDuration = 3000

export default {
  mixins: [resize],
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '500px'
    }
  },
  data() {
    return {
      chart: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      this.chart = echarts.init(this.$el, 'macarons')

      this.chart.setOption({
        tooltip: {
            trigger: "item",
            formatter: function(params) {
                var res = "";
                const name = ["内存", "容量", "物流", "拍照", "价格", "充电", "耳机", "像素", "流畅"];
                for (let i = 0; i < params.value.length; i++) {
                    var sentiment = "";
                    if (params.value[i] <= 2) {
                        sentiment = "负面";
                    }
                    else {
                        if (params.value[i] <=4) {
                            sentiment = "中性";
                        }
                        else {
                            sentiment = "正面";
                        }
                    }
                    res += name[i] + " : " + sentiment + "<br/>";
                }
                return res;
            }
        },
        radar: {
          radius: '66%',
          center: ['50%', '50%'],
          splitNumber: 8,
          splitArea: {
            areaStyle: {
              color: 'rgba(127,95,132,.3)',
              opacity: 1,
              shadowBlur: 45,
              shadowColor: 'rgba(0,0,0,.5)',
              shadowOffsetX: 0,
              shadowOffsetY: 15
            }
          },
          indicator: [
            { name: '内存', max: 5 },
            { name: '容量', max: 5 },
            { name: '物流', max: 5 },
            { name: '拍照', max: 5 },
            { name: '价格', max: 5 },
            { name: '充电', max: 5 },
            { name: '耳机', max: 5 },
            { name: '像素', max: 5 },
            { name: '流畅', max: 5 }
          ]
        },
        series: [{
          type: 'radar',
          symbolSize: 0,
          areaStyle: {
            normal: {
              shadowBlur: 13,
              shadowColor: 'rgba(0,0,0,.2)',
              shadowOffsetX: 0,
              shadowOffsetY: 10,
              opacity: 1
            }
          },
          data: [
            {
              value: [3, 3, 2, 4, 2, 4, 5, 3, 2],
              name: "各项参数评分"
            }
          ],
          animationDuration: animationDuration
        }]
      })
    }
  }
}
</script>
