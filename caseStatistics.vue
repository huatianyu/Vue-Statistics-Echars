<template>
  <v-hover v-slot:default="{hover}">
    <v-card :elevation="hover ? 24 : 2">
      <div
        id="case-statistics"
        class="echars-background"
        :style="{width: '100%'}"
      ></div> </v-card></v-hover
></template>
<script lang="ts">
import {Component, Vue, Inject, Prop, Watch} from 'vue-property-decorator';
import Util from '@/lib/util';
import AbpBase from '@/lib/abpbase';
import $ from 'jquery';
import echarts from 'echarts';

@Component({
  components: {},
})
export default class CaseStatistics extends AbpBase {
  caseStatistics: any = null;

  mounted() {
    this.caseStatisticsShow();
  }

  caseStatisticsShow() {
    if (this.caseStatistics != null) {
      return;
    }
    let self = this;

    // 科室量统计图表
    self.caseStatistics = echarts.init(
      document.getElementById('case-statistics')
    );

    self.caseStatistics.on('updateAxisPointer', function(event) {
      var xAxisInfo = event.axesInfo[0];
      if (xAxisInfo) {
        var dimension = xAxisInfo.value + 1;
        self.caseStatistics.setOption({
          series: {
            id: 'pie',
            label: {
              formatter: '{b}: {@[' + dimension + ']} ({d}%)',
            },
            encode: {
              value: dimension,
              tooltip: dimension,
            },
          },
        });
      }
    });
    self.caseStatistics.setOption({
      toolbox: {
        show: true,
        right: '20',
        top: 40, // icon标签的高度不能顶着顶部，不然会看不到title,所有还要设置一个 top值
        iconStyle: {
          normal: {
            textPosition: 'left',
          },
          emphasis: {
            textPosition: 'top',
          },
        },
        feature: {
          mark: {show: true},
          magicType: {show: true, type: ['line', 'bar'], right: 10},
          saveAsImage: {show: true},
        },
      },
      color: [
        '#d87c7c',
        '#919e8b',
        '#d7ab82',
        '#6e7074',
        '#61a0a8',
        '#efa18d',
        '#787464',
        '#cc7e63',
        '#724e58',
        '#4b565b',
      ],
      legend: {
        right: 40,
        top: -5,
        itemWidth: 15,
        width: '100%',
        selectedMode: true, //取消图例上的点击事件
        data: ['年份', '头部', '颈部', '胸部', '腹部', '盆腔', '四肢', '其他'],
        textStyle: {
          //图例文字的样式
          color: '#fff',
          fontSize: 10,
        },
      },
      tooltip: {
        trigger: 'axis',
        axisPointer: {
          type: 'cross',
          label: {
            backgroundColor: '#283b56',
          },
        },
      },
      dataset: {
        source: [
          ['年份', '2012', '2013', '2014', '2015', '2016', '2017'],
          ['头部', 41.1, 30.4, 65.1, 53.3, 83.8, 98.7],
          ['颈部', 86.5, 92.1, 85.7, 83.1, 73.4, 55.1],
          ['胸部', 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
          ['腹部', 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
          ['盆腔', 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
          ['四肢', 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
          ['其他', 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
        ],
      },
      xAxis: {
        type: 'category',
        axisLine: {
          lineStyle: {
            color: '#dcdee2',
          },
        },
      },
      yAxis: {
        gridIndex: 0,
        axisLine: {
          lineStyle: {
            color: '#dcdee2',
          },
        },
      },
      grid: {top: '55%', left: '15%', right: '15%'},
      title: {
        top: 30,
        subtext: '数据来自Rtis操作统计',
        left: 'center',
        text: '病例统计',
        textStyle: {
          fontWeight: 'normal', //标题颜色
          color: 'hsla(0, 0%, 100%, 0.7)',
        },
      },
      series: [
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,
          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,
          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,

          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,

          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,

          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,

          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },
        {
          type: 'bar',
          barWidth: 30,
          stack: '总量',
          smooth: true,

          seriesLayoutBy: 'row',
          label: {
            normal: {
              show: true,
              position: 'insideRight',
            },
          },
        },

        {
          type: 'pie',
          id: 'pie',
          radius: '30%',
          center: ['50%', '35%'],

          label: {
            formatter: '{b}: {@2012} ({d}%)',
          },
          encode: {
            itemName: '年份',
            value: '2012',
            tooltip: '2012',
          },
        },
      ],
    });
  }
}
</script>
<style scoped>
.echars-background {
  height: calc(40vh);
  background-image: url('../../../../public/img/icons/left-echarImg.png');
  background-size: 100% 100%;
}
.echars-background:hover {
  height: calc(40vh);
  background-image: url('../../../../public/img/icons/noGrid-left-echarImg.png');
  background-size: 100% 100%;
}
</style>
