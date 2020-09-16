<template>
  <v-row class="pa-4">
    <v-col class="py-0" cols="3">
      <v-row>
        <v-col cols="12">
          <department-statistics></department-statistics>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
          <task-statistics></task-statistics>
        </v-col>
      </v-row>
    </v-col>
    <v-col class="pa-0" cols="6">
      <v-row>
        <v-col cols="12">
          <effectiveness-statistics></effectiveness-statistics>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
          <upcoming-statistics></upcoming-statistics>
        </v-col>
      </v-row>
    </v-col>
    <v-col class="py-0" cols="3">
      <v-row
        ><v-col cols="12"><case-statistics></case-statistics></v-col>
      </v-row>
      <v-row
        ><v-col cols="12"><person-statistics></person-statistics></v-col>
      </v-row>
    </v-col>
  </v-row>
</template>
<script lang="ts">
import {Component, Vue, Inject, Prop, Watch} from 'vue-property-decorator';
import Util from '@/lib/util';
import AbpBase from '@/lib/abpbase';
import $ from 'jquery';
import StatisticsCard from '@/components/statistics-card/index';
import echarts from 'echarts';
import upcomingStatistics from './upcomingStatistics.vue';
import EffectivenessStatistics from './effectivenessStatistics.vue';
import TaskStatistics from './taskStatistics.vue';
import DepartmentStatistics from './departmentStatistics.vue';
import CaseStatistics from './caseStatistics.vue';
import PersonStatistics from './personStatistics.vue';
import './100.css';

@Component({
  components: {
    StatisticsCard,
    upcomingStatistics,
    EffectivenessStatistics,
    TaskStatistics,
    DepartmentStatistics,
    CaseStatistics,
    PersonStatistics,
  },
})
export default class Statistics extends AbpBase {}
</script>
<style scoped>
.echars-upcoming-height {
  height: calc(30vh);
}
</style>
