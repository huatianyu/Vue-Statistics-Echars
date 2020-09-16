<template>
  <v-hover v-slot:default="{hover}">
    <v-card :elevation="hover ? 24 : 2">
      <div
        id="department-statistics"
        class="echars-background"
        :style="{width: '100%'}"
      ></div>
    </v-card> </v-hover
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
export default class DepartmentStatistics extends AbpBase {
  departmentStatistics: any = null;

  mounted() {
    this.departmentShow();
  }

  //科室统计
  departmentShow() {
    if (this.departmentStatistics != null) {
      return;
    }
    let self = this;

    // 科室量统计图表
    self.departmentStatistics = echarts.init(
      document.getElementById('department-statistics')
    );
    self.departmentStatistics.on('updateAxisPointer', function(event) {
      var xAxisInfo = event.axesInfo[0];
      if (xAxisInfo) {
        var dimension = xAxisInfo.value + 1;
        self.departmentStatistics.setOption({
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
    self.departmentStatistics.setOption({
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
        left: 40,
        top: -5,
        selectedMode: true, //取消图例上的点击事件
        data: ['年份', '加速器1', '加速器2', '加速器3'],
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
          ['加速器1', 41.1, 30.4, 65.1, 53.3, 83.8, 98.7],
          ['加速器2', 86.5, 92.1, 85.7, 83.1, 73.4, 55.1],
          ['加速器3', 24.1, 67.2, 79.5, 86.4, 65.2, 82.5],
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
        subtext: '数据来自Rtis操作统计',
        top: 30,
        left: 'center',
        text: '科室统计',
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

        // {
        //   type: 'line',
        //   stack: '总量',
        //   smooth: true,
        //   name: '总计',
        //   data: [151.7, 189.7, 230.3, 222.8, 222.4, 236.3],
        //   seriesLayoutBy: 'row',
        //   label: {
        //     normal: {
        //       show: true,
        //       position: 'insideRight',
        //     },
        //   },
        // },
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
.echars-background:hover {
  height: calc(40vh);
  background-image: url('../../../../public/img/icons/noGrid-right-echarImg.png');
  background-size: 100% 100%;
}
.echars-background {
  height: calc(40vh);
  background-image: url('../../../../public/img/icons/right-echarImg.png');
  background-size: 100% 100%;
}
</style>
