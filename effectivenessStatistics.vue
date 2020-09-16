<template>
  <v-hover v-slot:default="{hover}">
    <v-card :elevation="hover ? 24 : 2">
      <div class="echars-all-background">
        <div class="echars-inner">
          <v-tabs dark background-color="#4dc9a875" vertical>
            <v-tab>
              <v-icon left>mdi-credit-card-multiple</v-icon>
              医师组
              <v-icon size="16" v-for="index in doctors">mdi-doctor</v-icon>
            </v-tab>
            <v-tab disabled>
              <v-icon left>mdi-access-point</v-icon>
              定位室<v-icon size="16" v-for="index in doctors"
                >mdi-washing-machine</v-icon
              >
            </v-tab>
            <v-tab disabled>
              <v-icon left>mdi-assistant</v-icon>
              计划室<v-icon size="16" v-for="index in doctors"
                >mdi-doctor</v-icon
              >
            </v-tab>
            <v-tab disabled>
              <v-icon left>mdi-package-variant-closed</v-icon>
              治疗组<v-icon size="16" v-for="index in doctors"
                >mdi-washing-machine</v-icon
              >
            </v-tab>
            <v-tab-item>
              <div
                id="effectiveness-statistics"
                class="echars-background"
              ></div>
            </v-tab-item>
          </v-tabs>
        </div>
      </div>
    </v-card>
  </v-hover>
</template>
<script lang="ts">
import {Component, Vue, Inject, Prop, Watch} from 'vue-property-decorator';
import Util from '@/lib/util';
import AbpBase from '@/lib/abpbase';
import $ from 'jquery';
import StatisticsCard from '@/components/statistics-card/index';
import echarts from 'echarts';
@Component({
  components: {},
})
export default class EffectivenessStatistics extends AbpBase {
  effectivenessStatistics: any = null;
  effectivenessStatisticsParams: any;
  doctors: Number[] = [1, 2, 3, 4];
  mounted() {
    this.effectivenessStatisticsShow();
  }

  effectivenessStatisticsShow() {
    var spirit = '';
    let dynamicData = [];
    if (this.effectivenessStatistics != null) {
      return;
    }
    let self = this;
    setTimeout(function() {
      // 任务量统计图表
      let dataSource = {
        chart: [
          {
            month: '2018-1',
            value: 380,
            patient: 4.3,
            doctor: 4,
          },

          {
            month: '2018-2',
            value: 390,
            patient: 4.4,
            doctor: 4,
          },

          {
            month: '2018-3',
            value: 400,
            patient: 4.5,
            doctor: 4,
          },

          {
            month: '2018-4',
            value: 421,
            patient: 4.8,
            doctor: 4,
          },

          {
            month: '2018-5',
            value: 432,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2018-6',
            value: 425,
            patient: 4.8,
            doctor: 4,
          },
          {
            month: '2018-7',
            value: 435,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2018-8',
            value: 434,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2018-9',
            value: 427,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2018-10',
            value: 450,
            patient: 5.1,
            doctor: 4,
          },

          {
            month: '2018-11',
            value: 439,
            patient: 5.0,
            doctor: 4,
          },

          {
            month: '2018-12',
            value: 450,
            patient: 5.1,
            doctor: 4,
          },
          {
            month: '2019-1',
            value: 380,
            patient: 4.3,
            doctor: 4,
          },

          {
            month: '2019-2',
            value: 390,
            patient: 4.4,
            doctor: 4,
          },

          {
            month: '2019-3',
            value: 400,
            patient: 4.5,
            doctor: 4,
          },

          {
            month: '2019-4',
            value: 421,
            patient: 4.8,
            doctor: 4,
          },

          {
            month: '2019-5',
            value: 432,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2019-6',
            value: 425,
            patient: 4.8,
            doctor: 4,
          },
          {
            month: '2019-7',
            value: 435,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2019-8',
            value: 434,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2019-9',
            value: 427,
            patient: 4.9,
            doctor: 4,
          },

          {
            month: '2019-10',
            value: 450,
            patient: 5.1,
            doctor: 4,
          },

          {
            month: '2019-11',
            value: 439,
            patient: 5.0,
            doctor: 4,
          },

          {
            month: '2019-12',
            value: 450,
            patient: 5.1,
            doctor: 4,
          },
        ],
      };

      let xAxisMonth = [],
        barData = [],
        lineData = [];
      for (let i = 0; i < dataSource.chart.length; i++) {
        xAxisMonth.push(dataSource.chart[i].month);
        barData.push({
          name: xAxisMonth[i],
          value: dataSource.chart[i].value,
          doctor: dataSource.chart[i].doctor,
        });
        lineData.push({
          name: xAxisMonth[i],
          value: dataSource.chart[i].patient,
          doctor: dataSource.chart[i].doctor,
        });
      }
      self.effectivenessStatistics = echarts.init(
        document.getElementById('effectiveness-statistics')
      );

      self.effectivenessStatistics.setOption({
        backgroundColor: '#020d2200',
        title: {
          text: '工作效率统计',
          top: 30,
          left: 'center',
          textStyle: {
            fontWeight: 'normal', //标题颜色
            color: 'hsla(0, 0%, 100%, 0.7)',
          },
        },
        grid: {
          top: '20%',
          left: '0%',
          right: '0%',
          bottom: '0%',
          containLabel: true,
        },

        xAxis: [
          {
            type: 'category',
            show: false,
            data: [
              '2018-1',
              '2018-2',
              '2018-3',
              '2018-4',
              '2018-5',
              '2018-6',
              '2018-7',
              '2018-8',
              '2018-9',
              '2018-10',
              '2018-11',
              '2018-12',
              '2019-1',
              '2019-2',
              '2019-3',
              '2019-4',
              '2019-5',
              '2019-6',
              '2019-7',
              '2019-8',
              '2019-9',
              '2019-10',
              '2019-11',
              '2019-12',
            ],
            axisLabel: {
              textStyle: {
                color: 'hsla(0, 0%, 100%, 0.7)',
              },
            },
          },

          {
            type: 'category',
            position: 'bottom',
            data: xAxisMonth,
            boundaryGap: true,
            // offset: 40,

            axisTick: {
              show: true,
            },
            axisLine: {
              show: true,

              lineStyle: {
                color: 'hsla(0, 0%, 100%, 0.7)',
              },
            },
            axisLabel: {
              interval: 0,
              rotate: 40,
              textStyle: {
                fontWeight: 'normal',
                fontSize: 12,
                color: 'hsla(0, 0%, 100%, 0.7)',
              },
            },
          },
        ],
        yAxis: [
          {
            name: '接诊总数',
            show: true,
            splitLine: {
              show: true,

              lineStyle: {
                color: 'hsla(0, 0%, 100%, 0.7)',
              },
            },
            axisTick: {
              show: true,
            },

            axisLine: {
              show: true,

              lineStyle: {
                color: 'hsla(0, 0%, 100%, 0.7)',
              },
            },
            axisLabel: {
              show: true,
              color: 'hsla(0, 0%, 100%, 0.7)',
            },
          },
          {
            show: true,
            type: 'value',
            name: '平均日接诊人次(个)',
            splitLine: {
              show: true,
              lineStyle: {
                color: 'yellow',

                type: 'dashed',
              },
            },
            nameTextStyle: {
              color: 'hsla(0, 0%, 100%, 0.7)',
              padding: [0, 0, 0, -50], //
            },
            axisLabel: {
              color: 'yellow',
              type: 'dashed',
            },
            axisTick: {
              show: true,
            },
            axisLine: {
              show: true,
              lineStyle: {
                color: 'yellow',
                type: 'dashed',
              },
            },
          },
        ],
        color: ['#e54035'],
        tooltip: {
          position: function(pos, params, dom, rect, size) {
            self.doctors = [];
            for (let i = 1; i <= params[0].data.doctor; i++) {
              self.doctors.push(i);
            }
          },
          trigger: 'axis',
          axisPointer: {
            type: 'none',
          },
          formatter: function(params) {
            return (
              params[0]['data'].name +
              '<br/>' +
              '<span style="display:inline-block;margin-right:5px;border-radius:10px;width:10px;height:10px;background: linear-gradient(to right, rgba(13,177,205,0.8) 0%, 50%,rgba(29,103,182,0.6) 51%,rgba(29,103,182,0.6) 100%);"></span>' +
              '月接诊总数: ' +
              params[1]['data'].value +
              '<br/>' +
              '<span style="display:inline-block;margin-right:5px;border-radius:10px;width:10px;height:10px;background-color:yellow;"></span>' +
              '平均日接诊人次: ' +
              params[0]['data'].value +
              '<br/>' +
              '&#9823' +
              '医师人数: ' +
              params[0]['data'].doctor
            );
          },
        },
        series: [
          {
            name: '训练人次',
            type: 'pictorialBar',
            xAxisIndex: 1,
            barCategoryGap: '-5%',
            symbol: 'path://d="M150 50 L130 130 L170 130  Z"',
            itemStyle: {
              normal: {
                color: function(params) {
                  let colorList = [
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                    'rgba(13,177,205,0.8)',
                    'rgba(29,103,182,0.6)',
                  ];
                  return colorList[params.dataIndex];
                },
              },
              emphasis: {
                opacity: 1,
              },
            },
            data: barData,
          },
          {
            name: '直接访问',
            type: 'bar',
            barWidth: '20%',
          },
          {
            symbol:
              'image://data:image/png;base64,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',
            symbolSize: 15,
            name: '完成率',
            type: 'line',
            yAxisIndex: 1,
            data: lineData,
            itemStyle: {
              normal: {
                borderWidth: 0,
                color: {
                  colorStops: [
                    {
                      offset: 0,
                      color: 'yellow',
                    },

                    {
                      offset: 0,
                      color: 'yellow',
                    },
                  ],
                },
              },
            },
          },
        ],
      });
    }, 0);
  }
}
</script>
<style scoped>
.echars-background {
  height: calc(40vh);
  /* background-image: url('../../../../public/img/icons/right-echarImg.png');
  background-size: 100% 100%; */
}

.echars-all-background {
  /* height: calc(40vh); */
  background-image: url('../../../../public/img/icons/center-ehcarImg.png');
  background-size: 100% 100%;
  /* padding: 10px, 10px, 10px, 10px; */
}

.echars-inner {
  padding: 50px;
}
</style>
