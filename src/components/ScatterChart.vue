<template>
 <v-container fluid>
 <v-card
   class="mx-auto"
   elevation="2"
   fluid                          
 >
 <v-card-title> {{title}} </v-card-title>
 <v-card-text> {{ msg }}</v-card-text>
  <Scatter
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
</v-card>
</v-container>  
</template>

<script>
import { Scatter } from 'vue-chartjs'
import { Chart as ChartJS, Title, Tooltip, Legend, LineElement, CategoryScale, PointElement, LinearScale } from 'chart.js'

ChartJS.register(Title, Tooltip, Legend, LineElement, CategoryScale, PointElement, LinearScale)

export default {
  name: 'ScatterChart',
  components: { Scatter },
  props: {
    title: {
      type:String,
      default:''
    },
    msg: {
      type:String,
      default:''
    },
    chartData: {
        type: Object,
        required: true
      },
    chartOptions: {
      type: Object,
      default: () => {}
    },
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
      default: 500
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
      type: Object,
      default: () => {}
    }
  },

}
/* 
data() {
    return {
      chartData: {
        label: [ 'January', 'February', 'March' ],
        data: [
              {
                x: -2,
                y: 4
              },
              ]
      },
      chartOptions: {
        responsive: true
      }
    }
  },
*/
</script>