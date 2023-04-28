<template>
  <div class="mapMain">
    <section class="section">
      <div id="map" :style="{ height: '560px', width: '100%' }"></div>
    </section>
  </div>
</template>

<script>
import * as echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
import 'echarts/map/js/china.js'

export default {
  name: 'EChartMapContainer',
  data() {
    return {
      provinceData: [],
    }
  },
  mounted() {
    this.getProvinceData()
    this.init()
  },
  methods: {
    getProvinceData: async function () {
      //var r = await this.$root.api_get('/api/v1/counter-history/?name=qr-verify-ok');
      var r = { data: { data: [{ name: '北京',value: '30'  }, { name: '上海',value: '40'  }, { name: '广东',value: '60'  }] } }
      var ok_data = r.data.data
      this.provinceData = ok_data
    },
    init() {
      // 基于准备好的dom，初始化echarts实例
      let chinaMap = echarts.init(document.getElementById('map'))
      window.onresize = chinaMap.resize // 窗口或框架被调整大小时执行chinaMap.resize
      chinaMap.setOption({
        tooltip: {
          trigger: 'item',
          formatter: function (e, t, n) {
            return e.value == 'NaN'
              ? e.name + '：' + '0'
              : e.name + '：' + e.value
          },
        },
        legend: {
          orient: 'vertical',
          left: 'left',
        },
        visualMap: {
          min: 0,
          max: 10000,
          left: 10,
          bottom: 10,
          showLabel: !0,
          text: ['高', '低'],
          textStyle: {
            color: '#231d6b',
          },
          pieces: [
            {
              gt: 100,
              label: '> 100',
              color: '#4735df',
            },
            {
              gte: 70,
              lte: 100,
              label: '70 - 100',
              color: '#5f4fe7',
            },
            {
              gte: 40,
              lte: 70,
              label: '40 - 70',
              color: '#7d70e7',
            },
            {
              gte: 10,
              lte: 40,
              label: '10 - 40',
              color: '#bbb5ef',
            },
            {
              gte: 1,
              lt: 10,
              label: '1 - 10',
              color: '#cbc8ec',
            },
            {
              gt: 0,
              lt: 1,
              label: '1',
              color: '#dad8f2',
            },
            {
              value: 0,
              color: '#ffffff',
            },
          ],
          show: !0,
        },
        toolbox: {
          show: true,
          orient: 'vertical',
          left: 'right',
          top: 'center',
          feature: {
            dataView: { readOnly: false },
            restore: {},
            saveAsImage: {},
          },
        },
        geo: {
          map: 'china',
          roam: !1,
          scaleLimit: {
            min: 1,
            max: 2,
          },
          zoom: 1.23,
          // top: 120,
          label: {
            normal: {
              show: !0,
              fontSize: '14',
              color: 'rgba(0,0,0,0.7)',
            },
          },
          itemStyle: {
            normal: {
              //shadowBlur: 50,
              //shadowColor: 'rgba(0, 0, 0, 0.2)',
              borderColor: 'rgba(0, 0, 0, 0.2)',
            },
            emphasis: {
              areaColor: '#f2d5ad',
              shadowOffsetX: 0,
              shadowOffsetY: 0,
              borderWidth: 0,
            },
          },
        },
        series: [
          {
            type: 'map',
            mapType: 'china',
            roam: false,
            geoIndex: 0,
            label: {
              normal: {
                show: true,
              },
              emphasis: {
                show: true,
              },
            },
            data: this.provinceData,
          },
        ],
      })
    },
  },
}
</script>
<style>
.mapMain {
  height: 100%;
  width: 100%;
}
</style>
