<!--
 描述: 人才队伍
 作者: Jack Chen
 日期: 2020-05-09
-->

<template>
    <div class="map">
    <div class="chart" id="chart_left22"></div>
    <div class="map1"></div>
    <div class="map2"></div>
    <div class="map3"></div>
  </div>
</template>

<script>
export default {
  name: "secondary",
  data() {
    return {
      
    }
  },
  mounted() {
    this.getEchartLeft2();
  },
  methods: {
    getEchartLeft2() {
      let myChart = echarts.init(document.getElementById('chart_left22'));
      let scaleData = [{
        name: '居住用地2',
        value: 10.34
      },{
        name: '商业用地',
        value: 21.45
      },{
        name: '工业用地',
        value: 24.89
      },{
        name: '科研用地',
        value: 2.34
      },{
        name: '其它用地',
        value: 5.21
      }];
      let rich = {
        white: {
          color: '#ddd',
          align: 'center',
          padding: [3, 0]
        }
      };
      let placeHolderStyle = {
        normal: {
          label: {
            show: false
          },
          labelLine: {
            show: false
          },
          color: 'rgba(0, 0, 0, 0)',
          borderColor: 'rgba(0, 0, 0, 0)',
          borderWidth: 0
        }
      };
      let data = [];
      let color=['#00ffff', '#00cfff', '#006ced', '#ffe000', '#ffa800', '#ff5b00', '#ff3000']
      for (let i = 0; i < scaleData.length; i++) {
        data.push({
          value: scaleData[i].value,
          name: scaleData[i].name,
          itemStyle: {
            normal: {
              borderWidth: 6,
              shadowBlur: 10,
              borderColor: color[i],
              shadowColor: color[i]
            }
          }
        }, {
          value: 2,
          name: '',
          itemStyle: placeHolderStyle
        });
      }

      let option = {
        series: [{
          name: '',
          type: 'pie',
          clockWise: false,
          radius: ['66%', '68%'],
          center: ['50%', '50%'],
          hoverAnimation: false,
          itemStyle: {
            normal: {
              label: {
                show: true,
                position: 'outside',
                color: '#ddd',
                formatter: (params) => {
                  let percent = 0;
                  let total = 0;
                  for (let i = 0; i < scaleData.length; i++) {
                    total += scaleData[i].value;
                  }
                  percent = ((params.value / total) * 100).toFixed(0);
                  if (params.name !== '') {
                    return params.name + '\n{white|' + '占比' + percent + '%}';
                  } else {
                    return '';
                  }
                },
                rich: rich
              },
              labelLine: {
                length: 10,
                length2: 30,
                show: true,
                color: '#00ffff'
              }
            }
          },
          data: data
        }]
      }

      myChart.setOption(option, true);
      window.addEventListener('resize', () => {
        myChart.resize();
      });
    },
  },
  beforeDestroy() {
    
  }
};
</script>

<style lang="scss" scoped>
.talent-container {
  .chart {
    height: 3rem;
  }
}
 .map {
  position: relative;
  height: 10.125rem;

  .chart {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 5;
    height: 10.125rem;
    width: 100%;
  }
  %map-style {
          position: absolute;
          top: 50%;
          left: 50%;
          transform: translate(-50%, -50%);
          width: 6.475rem;
          height: 6.475rem;
          background: url(../../assets/img/brand/map.png) no-repeat;
          background-size: 100% 100%;
          opacity: 0.3;
        }
  .map1 {
    @extend %map-style;
  }

  .map2 {
    @extend %map-style;
    width: 8.0375rem;
    height: 8.0375rem;
    background-image: url(../../assets/img/brand/lbx.png);
    opacity: 0.6;
    -webkit-animation: rotate 15s linear infinite;
    animation: rotate 15s linear infinite;
    z-index: 2;
  }

  .map3 {
    @extend %map-style;
    width: 7.075rem;
    height: 7.075rem;
    background-image: url(../../assets/img/brand/jt.png);
    -webkit-animation: rotate1 10s linear infinite;
    animation: rotate1 10s linear infinite;
  }
}
</style>
