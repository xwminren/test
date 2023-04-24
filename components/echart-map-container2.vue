<template>
    <div class="echart">
      <div class="content">
        <div id="map_cn"></div>
      </div>
    </div>
  </template>
   
  <script>
    import * as echarts from "echarts";
    
    import china from "@/assets/json/china.json"
   
    export default {
      name: 'EChartMapContainer2',
      data() {
        return {
          //地图中的数据
          dataList: [
            {
              name: "南海诸岛",
              value: 25,
            },
            {
              name: "北京",
              value: 71,
            },
            {
              name: "天津",
              value: 52,
            },
            {
              name: "上海",
              value: 14,
            },
            {
              name: "重庆",
              value: 50,
            },
            {
              name: "河北",
              value: 20,
            },
            {
              name: "河南",
              value: 30,
            },
            {
              name: "云南",
              value: 55,
            },
            {
              name: "辽宁",
              value: 50,
            },
            {
              name: "黑龙江",
              value: 40,
            },
            {
              name: "湖南",
              value: 6,
            },
            {
              name: "安徽",
              value: 96,
            },
            {
              name: "山东",
              value: 75,
            },
            {
              name: "新疆",
              value: 45,
            },
            {
              name: "江苏",
              value: 15,
            },
            {
              name: "浙江",
              value: 8,
            },
            {
              name: "江西",
              value: 78,
            },
            {
              name: "湖北",
              value: 78,
            },
            {
              name: "广西",
              value: 36,
            },
            {
              name: "甘肃",
              value: 25,
            },
            {
              name: "山西",
              value: 140,
            },
            {
              name: "内蒙古",
              value: 85,
            },
            {
              name: "陕西",
              value: 85,
            },
            {
              name: "吉林",
              value: 74,
            },
            {
              name: "福建",
              value: 20,
            },
            {
              name: "贵州",
              value: 74,
            },
            {
              name: "广东",
              value: 47,
            },
            {
              name: "青海",
              value: 45,
            },
            {
              name: "西藏",
              value: 41,
            },
            {
              name: "四川",
              value: 3,
            },
            {
              name: "宁夏",
              value: 7,
            },
            {
              name: "海南",
              value: 7,
            },
            {
              name: "台湾",
              value: 200,
            },
            {
              name: "香港",
              value: 2,
            },
            {
              name: "澳门",
              value: 5,
            }
          ],
          //指定图表的配置项和数据
          option: {
            //标题组件
            title: {
              show: true,
              text: '全国各省份旅游景点(已评级)数量',
              subtext: '截至到2021年12月',
              left: "center",
              top: 16,
            },
            //提示框组件
            tooltip: {
              show: true,
              //触发类型：数据项图形触发
              trigger: 'item',
              padding: 10,
              borderWidth: 1,
              borderColor: '#409eff',
              backgroundColor: 'rgba(255,255,255,0.4)',
              textStyle: {
                color: '#000000',
                fontSize: 12
              },
              //提示框内容格式器
              formatter: (e) => {
                let data = e.data;
                //此处将各等级景点数量表示为0-10内的随机整数
                data.five = Math.random() * 10 | 0;
                data.four = Math.random() * 10 | 0;
                data.three = Math.random() * 10 | 0;
                data.two = Math.random() * 10 | 0;
                data.one = Math.random() * 10 | 0;
                //景点数量 - 五个等级之和
                data.number = data.five + data.four + data.three + data.two + data.one;
                //字符串模板
                let context = `
                 <div>
                     <p style="line-height: 30px; font-weight: 600">${data.name}</p>
                     <p><span>景点数量 : </span><span>${data.number}处</span></p>
                     <p><span>5A级 : </span><span>${data.five}处</span></p>
                     <p><span>4A级 : </span><span>${data.four}处</span></p>
                     <p><span>3A级 : </span><span>${data.three}处</span></p>
                     <p><span>2A级 : </span><span>${data.two}处</span></p>
                     <p><span>1A级 : </span><span>${data.one}处</span></p>
                 </div>
              `;
                return context;
              }
            },
            //视觉映射组件(左下角)
            visualMap: {
              show: true,
              left: 26,
              bottom: 40,
              showLabel: true,
              // 是否显示拖拽用的手柄（手柄能拖拽调整选中范围）
              calculable: false,
              // 拖拽时，是否实时更新
              realtime: true,
              align: 'left',
              //各颜色代表的区域
              pieces: [
                {
                  gte: 100,
                  label: "> 100",
                  color: "#FDB669"
                },
                {
                  gte: 50,
                  lt: 99,
                  label: "50 - 99",
                  color: "#FECA7B"
                },
                {
                  gte: 30,
                  lt: 49,
                  label: "30 - 49",
                  color: "#FEE191"
                },
                {
                  gte: 10,
                  lt: 29,
                  label: "10 - 29",
                  color: "#FFF0A8"
                },
                {
                  lt: 9,
                  label: '< 10',
                  color: "#FFFFBF"
                }
              ]
            },
            //地理坐标系组件
            geo: {
              //使用 registerMap 注册的地图名称
              map: "china",
              //是否开启鼠标缩放和平移漫游
              roam: true,
              //当前视角缩放比例
              zoom: 1,
              //滚轮缩放的极限控制
              scaleLimit: {
                min: 1, //最小1倍
                max: 3 //最大3倍
              },
              //地图组件离容器的距离
              top: 90,
              left: 'center',
              //图形上的文本标签
              label: {
                show: true,
                fontSize: "11"
              },
              //地图区域的多边形 图形样式
              itemStyle: {
                borderColor: "rgba(0, 0, 0, 0.2)",
                shadowColor: 'rgba(0, 0, 0, 0.2)',
                shadowBlur: 10,
                // 高亮状态(鼠标移入后)的多边形和标签样式
                emphasis: {
                  areaColor: "#f98333",
                  shadowOffsetX: 2,
                  shadowOffsetY: 2,
                },
              }
            },
            series: [
              {
                type: "map",
                roam: true,
                geoIndex: 0,
                data: '',
                label: {
                  show: true,
                }
              }
            ]
          },
        };
      },
   
      methods: {
        //定义方法 draw_map 绘制中国地图
        draw_map() {
          echarts.registerMap('china', china)
          let myChart = echarts.init(document.getElementById('map_cn'));
          //高亮轮播展示
          var hourIndex = 0;
          var carouselTime = null;
          //setInterval() 可在每隔指定的毫秒数循环调用函数或表达式,直到clearInterval把它清除
   
          //使用setInterval方法后,必须使用箭头函数而不能写function,否则后续在该方法中无法调用data中的数据
          //carouselTime =setInterval(function(){ //错误写法
   
          carouselTime = setInterval(() => {
            //dispatchAction echarts的API：触发图表行为
            myChart.dispatchAction({
              type: "downplay", //downplay 取消高亮指定的数据图形
              seriesIndex: 0
            });
            myChart.dispatchAction({
              type: "highlight", //highLight 高亮指定的数据图形
              seriesIndex: 0, //系列index
              dataIndex: hourIndex //数据index
            });
            myChart.dispatchAction({
              type: "showTip", //showTip 显示提示框
              seriesIndex: 0,
              dataIndex: hourIndex
            });
            hourIndex++;
            //当循环到数组当中的最后一条数据后，重新进行循环
            if (hourIndex > this.dataList.length) {
              hourIndex = 0;
            }
          }, 3000);
          //鼠标移入组件时停止轮播
          myChart.on("mousemove", (e) => {
            clearInterval(carouselTime); //清除循环
            myChart.dispatchAction({
              type: "downplay",
              seriesIndex: 0,
            });
            myChart.dispatchAction({
              type: "highlight",
              seriesIndex: 0,
              dataIndex: e.dataIndex
            });
            myChart.dispatchAction({
              type: "showTip",
              seriesIndex: 0,
              dataIndex: e.dataIndex
            });
          });
          //鼠标移出组件时恢复轮播
          myChart.on("mouseout", () => {
            carouselTime = setInterval(() => {
              myChart.dispatchAction({
                type: "downplay",
                seriesIndex: 0,
   
              });
              myChart.dispatchAction({
                type: "highlight",
                seriesIndex: 0,
                dataIndex: hourIndex
              });
              myChart.dispatchAction({
                type: "showTip",
                seriesIndex: 0,
                dataIndex: hourIndex
              });
              hourIndex++;
              if (hourIndex > this.dataList.length) {
                hourIndex = 0;
              }
            }, 3000);
          });
   
          //显示地图
          myChart.setOption(this.option);
        },
   
        //修改echart配制
        setEchartOption() {
          this.option.series[0].data = this.dataList;
        },
      },
      created() {
        this.setEchartOption();
      },
      mounted() {
        this.$nextTick(() => {
          this.draw_map();
        });
      }
    };
  </script>
   
  <style >
    .echart {
      width: 100%;
      height: 200px;
    }
    .echart .content {
        width: 95.8%;
        height: 96%;
        margin: auto;
    }
    #map_cn {
        width: 65%;
        height: 100%;
        background-color: #eaeaea;
        margin: auto;
    }
  </style>
