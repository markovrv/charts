<template>
  <Bar
    :chart-options="chartOptions"
    :chart-data="chartData"
    :chart-id="chartId"
    :dataset-id-key="datasetIdKey"
    :plugins="plugins"
    :css-classes="cssClasses"
    :styles="styles"
    :width="width"
    :height="height"
  />
</template>

<script>
import { Bar } from 'vue-chartjs/legacy'

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale
} from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale)

export default {
  name: 'BarChart',
  components: {
    Bar
  },
  props: {
    chartId: {
      type: String,
      default: 'bar-chart'
    },
    datasetIdKey: {
      type: String,
      default: 'label'
    },
    width: {
      type: Number,
      default: 400
    },
    height: {
      type: Number,
      default: 400
    },
    cssClasses: {
      default: '',
      type: String
    },
    styles: {
      type: Object,
      default: () => {}
    },
    plugins: {
      type: Array,
      default: () => []
    },
    dataset: Array
  },
  data() {
    return {
      chartData: {
        labels: [
          '2',
          '3',
          '4',
          '5',
        ],
        datasets: [
          {
            label: 'group A',
            backgroundColor: '#41B883',
            data: [0, 0, 0, 0]
          },
          {
            label: 'group B',
            backgroundColor: '#E46651',
            data: [0, 0, 0, 0]
          },
          {
            label: 'group C',
            backgroundColor: '#00D8FF',
            data: [0, 0, 0, 0]
          },
          {
            label: 'group D',
            backgroundColor: '#DD1B16',
            data: [0, 0, 0, 0]
          },
        ]
      },
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      }
    }
  },
  created() {
    this.dataset.forEach(student => {
      var col = 0;

           if (student.race.ethnicity == "group A") col = 0;
      else if (student.race.ethnicity == "group B") col = 1;
      else if (student.race.ethnicity == "group C") col = 2;
      else if (student.race.ethnicity == "group D") col = 3;

           if (student["math score"] < 25) this.chartData.datasets[col].data[0]++;
      else if (student["math score"] < 50) this.chartData.datasets[col].data[1]++;
      else if (student["math score"] < 75) this.chartData.datasets[col].data[2]++;
      else                                 this.chartData.datasets[col].data[3]++;
    });
  }
}
</script>
