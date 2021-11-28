<template>
  <div class="chart-one">
    <div>
      <highcharts :options="chartOptions" ref="chartComponent"></highcharts>
    </div>
  </div>
</template>

<script>
import {Chart} from 'highcharts-vue';
import axios from 'axios';
export default {
  name: "Chart",
  data() {
    return {
      chartOptions: {
        chart: {
          type: 'spline',
          height: '700px',
        },
        title: {
          text: 'WEEKLY RETENTION CURVES'
        },
        xAxis: {
          title: {
            enabled: true,
            text: 'Steps in the Onboarding Flow'
          },
          labels: {
            format: '{value} %',
          },
          accessibility: {
            rangeDescription: 'Range: 0 to 80 km.'
          },
          max: 100,
          min: 0,
        },
        yAxis: {
          title: {
            text: 'Percentage of users'
          },
          labels: {
            format: '{value} %',
          },
          step: 10,
          max: 100,
          min: 0,
        },
        legend: {
          align: 'center',
          verticalAlign: 'top',
          layout: 'horizontal',
          x: 0,
          y: 50
        },
        plotOptions: {
          spline: {
            marker: {
              enabled: false
            }
          }
        },
        series: []
      }
    }
  },
  components: {
    highcharts: Chart
  },
  mounted () {
    axios.get('http://localhost:8000/weekly-retention-data?start_date=2016-07-19&end_date=2016-08-10')
        .then((response) => {
          this.chartOptions.series = response.data.data;
          this.redrawChart();
        })
  },
  methods: {
    redrawChart() {
      this.$refs.chartComponent.chart.redraw();
    }
  }
};
</script>