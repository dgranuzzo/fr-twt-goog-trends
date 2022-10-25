<template>
<v-app>
  <!--
    <v-navigation-drawer app>
    
    <router-view></router-view>
    Menu
  </v-navigation-drawer>

  <v-app-bar app>
    
    app-bar
  </v-app-bar>
  -->
  <!-- Sizes your content based upon application components -->
  <v-main>

    <!-- Provides the application the proper gutter -->
    <v-container fluid>
            <v-card
                elevation="2"
                fluid
            >
                <v-card-title> Texto para pesquisa </v-card-title>
                  <v-row
                    class="pa-2"
                    justify="center"
                    align="center"
                  >
                  <v-col class="d-flex" cols="12" sm="12" >
                        <v-text-field
                          label="search string"
                          v-model="searchString"
                          hide-details="auto"
                        ></v-text-field>
                  </v-col>
                  <v-col class="d-flex" cols="4" sm="4" >
                    <v-switch
                      v-model="switchTwitter"
                      label="Twitter"
                    ></v-switch>
                  </v-col>
                  <v-col class="d-flex" cols="4" sm="4" >
                    <v-switch
                      v-model="switchGTrends"
                      label="Google Trends"
                    ></v-switch>
                  </v-col>
                  <v-col class="d-flex" cols="4" sm="4" >
                    <v-switch
                      v-model="switchGNews"
                      label="Google News"
                    ></v-switch>
                  </v-col>
                  </v-row>

                  <!-- Tables -->
                  <v-row
                    class="pa-2"
                    justify="center"
                    align="center"
                  >
                  <v-col class="d-flex" cols="12" sm="12" >
                  <v-tabs>
                    <v-tab>Google Trends</v-tab>
                    <v-tab>Google News</v-tab>
                    <v-tab>Twitter</v-tab>
                    <v-tab>Dashboard</v-tab>
                    <v-tab-item>
                      <v-container fluid>
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                      </v-row>
                      <v-row
                          class="pa-2"
                          justify="center"
                          align="center"
                         >
                          <v-col class="d-flex" cols="12" sm="12" >
                            <v-data-table
                              :headers="headersGTrendsTodayHot"
                              :items="itemsGTrendsTodayHot"
                              :items-per-page="10"
                              class="elevation-1"
                            ></v-data-table>
                           </v-col>
                      </v-row>
                      </v-container>
                    </v-tab-item>
                    <v-tab-item>
                      <!-- Tables News -->
                      <v-container fluid>
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                      </v-row>
                      <v-row
                          class="pa-2"
                          justify="center"
                          align="center"
                         >
                          <v-col class="d-flex" cols="12" sm="12" >
                            <v-data-table
                              :headers="headersGNews"
                              :items="itemsGNews"
                              :items-per-page="5"
                              class="elevation-1"
                            ></v-data-table>
                           </v-col>
                      </v-row>
                      </v-container>
                    </v-tab-item>
                    <v-tab-item>
                      <!-- Tables Twitter -->
                      <v-container fluid>
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                      </v-row>
                      <v-row
                          class="pa-2"
                          justify="center"
                          align="center"
                         >
                          <v-col class="d-flex" cols="12" sm="12" >
                            <v-data-table
                              :headers="headersTwitter"
                              :items="itemsTwitter"
                              :items-per-page="10"
                              class="elevation-1"
                            ></v-data-table>
                           </v-col>
                           <v-col class="d-flex" cols="12" sm="12" >
                            <v-data-table
                              :headers="headersTwitterTrends"
                              :items="itemsTwitterTrends"
                              :items-per-page="10"
                              class="elevation-1"
                            ></v-data-table>
                           </v-col>
                      </v-row>
                      </v-container>
                    </v-tab-item>
                    <v-tab-item>
                  <!-- CHARTS -------- -->
                    <v-container fluid>
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                        <v-col class="d-flex" cols="6" sm="6" >
                          <BarChart 
                              ref="bar-chart" 
                              chartId="Time Variation"
                              :chartData="twitterTrendsBarChartData"
                              :chartOptions="BarChartOptions"
                            />
                        </v-col>

                        <v-col class="d-flex" cols="6" sm="6" >
                          <BarChart 
                              ref="bar-chart" 
                              chartId="Time Variation"
                              :chartData="googleTrendsBarChartData"
                              :chartOptions="BarChartOptions"
                            />
                        </v-col>

                        <v-col class="d-flex" cols="6" sm="6" >
                          <LineChart
                            :chartOptions='LineChartOptions'
                            :chartData='LineChartData'
                            chart-id='myCustomId'
                            ref="line-chart"
                          />
                        </v-col>
                        <v-col class="d-flex" cols="6" sm="6" >
                          <DoghnutChart
                            :chartOptions='LineChartOptions'
                            :chartData='LineChartData'
                            chart-id='myCustomId'
                            ref="line-chart"
                          />
                        </v-col>

                      </v-row>
                      </v-container>                  
                     </v-tab-item>
                  </v-tabs>
                  </v-col>
                  </v-row>

                  <v-row
                    class="pa-2"
                    justify="center"
                    align="center"
                  >
                    <v-col class="d-flex" cols="12" sm="12" >
                    <v-btn
                      color="primary"
                      @click="searchData()"
                    >
                      Pesquisar
                    </v-btn>
                    </v-col>
                  </v-row>
            </v-card>
                 <v-row
                    class="pa-2"
                    justify="center"
                    align="center"
                  >
                    <v-col class="d-flex" cols="12" sm="12" >
                    {{ errorMsg }}
                    </v-col>
                  </v-row>
    </v-container>
  </v-main>

  <v-footer padless>
    <v-col
      class="text-center"
      cols="12"
    >
      {{ new Date().getFullYear() }} — <strong>consultas</strong>
    </v-col>
  </v-footer>
  <!-- 
                        <v-switch
                      v-model="switchTwitter"
                      :label="`Pesquisar Twitter: ${switchTwitter.toString()}`"
                    ></v-switch>
  -->
<!-- dialog performing request -->   
    <v-dialog
      v-model="performingRequest"
      max-width="350"
    >
      <v-card>
        <v-card-title class="headline">Pesquisando...</v-card-title>
        <v-card-text>
          <template>
            <div class="text-center">
              <v-progress-circular
                :size="50"
                color="primary"
                indeterminate
              ></v-progress-circular>
            </div>
          </template>    
        </v-card-text>
      </v-card>
    </v-dialog> 
</v-app>
</template>

<script>
//import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'
import BarChart from '@/components/BarChart.vue'
import LineChart from '@/components/LineChart.vue'
import DoghnutChart from '@/components/DoghnutChart.vue'

const headers = {
    'Content-Type': 'application/json',
    'Access-Control-Allow-Headers': '*',
    'Access-Control-Allow-Origin':'*'
}
const URL_BACK= process.env.VUE_APP_URL_BACK

const chartOptions= {
        responsive: true,
        maintainAspectRatio: false
}

export default {
  name: 'DashView',
  components: {
    BarChart,
    LineChart,
    DoghnutChart,
  },
  data() {
    return {
      errorMsg: '',
      performingRequest: false,
      switchTwitter: true,
      switchGTrends: true,
      switchGNews: true,

      searchString: "",
      
      headersGNews: [
        {
          text:'Título',
          align:'start',
          sortable: true,
          value:'title',
        },
        {
          text:'Meio',
          align:'start',
          sortable: true,
          value:'media',
        },

        {
          text:'Data',
          align:'start',
          sortable: true,
          value:'date',
        },
        {
          text:'Descrição',
          align:'start',
          sortable: false,
          value:'desc',
        },
        {
          text:'Link',
          align:'start',
          sortable: false,
          value:'link',
        },

      ],
      itemsGNews: [
      ],
      
      headersGTrendsTodayHot: [
        {
          text:'Título',
          align:'start',
          sortable: true,
          value:'title',
        },
        {
          text:'Tipo',
          align:'start',
          sortable: true,
          value:'type',
        },
      ],
      itemsGTrendsTodayHot: [],

      headersGTrendsRealTimeSearch:[
        {
          text:'Título',
          align:'start',
          sortable: false,
          value:'results',
        },
      ],
      itemsGTrendsRealTimeSearch: [],
      
      googleTrendsBarChartData: {},
      itemsGTrendsInterestTime: [],
      labelsGTrendsInterestTime: [],

      headersTwitter:[
            {
              text: 'Texto',
              align: 'start',
              sortable: false,
              value: 'text',
            },            
            {
              text: 'Data e hora',
              align: 'start',
              sortable: true,
              value: 'created_at',
            },            
            {
              text: 'Origem',
              align: 'start',
              sortable: false,
              value: 'source',
            },            
            {
              text: 'Retweets',
              align: 'start',
              sortable: true,
              value: 'retweet_count',
            },
            {
              text: 'Likes',
              align: 'start',
              sortable: true,
              value: 'favorite_count',
            },              
          ],
      itemsTwitter:[],
      headersTwitterTrends: [
            {
              text: 'Tendência',
              align: 'start',
              sortable: false,
              value: 'name',
            }, 
            {
              text: 'Tweet Volume',
              align: 'start',
              sortable: false,
              value: 'tweet_volume',
            },                        
            {
              text: 'Data',
              align: 'start',
              sortable: false,
              value: 'timestamp',
            }, 
      ],
      itemsTwitterTrends:[],

      BarChartDataOrig: {
        labels: [ 'January', 'February', 'March'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [40, 20, 12]
          },
          {
            label: 'Data Two',
            backgroundColor: '#f87979',
            data: [22,55,34]
          },
        ]
      },
      
      BarChartOptions: chartOptions,
      LineChartOptions: chartOptions,
      LineChartData:{
        labels: [ 'Jan', 'Feb', 'Mar'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: '#f87979',
            data: [40, 20, 12]
          }
        ]
      }, 
      BarChartDataEx: {
        labels: [],
        datasets: [
          {
            label: 'Tweets',
            backgroundColor: '#f87979',
            data: []
          },
        ]
      },

      twitterTrendsBarChartData: {},
      //twitterTrendsBarChartDataSet: [],
      //twitterTrendsBarChartLabels: [],
    }
  },
  methods: {
    searchGNews() {
        this.performingRequest = true
        let url = URL_BACK + "google_news?query=" + this.searchString
        console.log(url)

      let vueInstance = this
      axios.get(url, {
           headers: headers
         }).then(response => {
           vueInstance.performingRequest = false
           vueInstance.itemsGNews = response.data.search_results
           console.log(vueInstance.itemsGNews)
         }, (error) => {
          console.log(error)
          this.performingRequest = false
          console.log("ERRO NEWS")
         })
     },
    searchGTrends() {
      console.log('g trends hot')
      this.performingRequest = true
      //let url = this.URL_BACK + "gt_realtime"?query=" + this.location //gt_hot
      let url = URL_BACK + "google_trends_three?query=" + this.searchString
      console.log(url)
      let vueInst = this
      axios.get(url, {
           headers: headers
         }).then(response => {
           console.log(response)
           vueInst.performingRequest = false
           //vueInst.itemsGTrendsTodayHotTrends = response.data.results.results
           vueInst.itemsGTrendsTodayHot = response.data.today_hot_trends.results
           vueInst.itemsGTrendsInterestTime = response.data.int_over_time.results
           vueInst.itemsGTrendsRealTimeSearch = response.data.realtime_searches.results
           
           let nodes = vueInst.itemsGTrendsInterestTime[vueInst.searchString]
           let dataLabels = []
           let dataSet = []
                      
           if (response.data.int_over_time.status == "ok") {
            Object.entries(nodes).forEach(([key, value]) => {
              //console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
              dataLabels.push(key.toString().slice(0,10))
              dataSet.push(value)
            });
            vueInst.googleTrendsBarChartData = this.createChartDataObj(dataLabels, dataSet, 'Google Trends Interest Over Time')
           } else {
            console.log('error else')
            this.errorMsg = vueInst.itemsGTrendsInterestTime.results
           }
         }, (error) => {
          console.log(error)
          this.performingRequest = false
          console.log("ERRO GT_HOT")
         })
    }, 
    searchTwitter() {
      console.log('twitter')
      this.performingRequest = true
      //let url = this.URL_BACK + "gt_realtime"?query=" + this.location
      let url = URL_BACK + "twt_search?query=" + this.searchString
      let vueInst = this
      axios.get(url, {
           headers: headers
         }).then(response => {
           console.log(response)
           vueInst.performingRequest = false
           vueInst.itemsTwitter = response.data.results
           vueInst.itemsTwitterTrends = response.data.trends
           let nodes = response.data.trends
           /* Map each item of nodes to a nested array where each is a row of two columns */
           let dataLabels = nodes.map((node) => [node.name]);
           let dataSet = nodes.map((node) => [node.tweet_volume]);
           vueInst.twitterTrendsBarChartData = this.createChartDataObj(dataLabels, dataSet, 'Tweets volume')
         }, (error) => {
          console.log(error)
          this.performingRequest = false
          console.log("ERRO TWITTER")
         })
    },     

    searchData() {
      console.log(this.switchGtrnends)
      if (this.switchGNews === true) {
        this.searchGNews()
      }
      if (this.switchGTrends === true) {
      this.searchGTrends()      
      }
      if (this.switchTwitter === true) {
        this.searchTwitter()
      }
     
    },

    createChartDataObj(labelsArr, dataArr, label) {
      let ChartData= {
        labels: labelsArr,
        datasets: [
          {
            label: label,
            backgroundColor: '#f87979',
            data: dataArr
          },
        ]
      }
      return ChartData
    },

    requestData () {
      axios.get(`https://api.npmjs.org/downloads/range/${this.period}/${this.package}`)
      .then(response => {
        this.downloads = response.data.downloads.map(download => download.downloads)
        this.labels = response.data.downloads.map(download => download.day)
        this.packageName = response.data.packagethis.loaded = true})
      .catch(err => {
        this.errorMessage = err.response.data.error
        this.showError = true})
    },

  },
  created() {
    console.log(process.env.BASE_URL)
    //console.log(URL_BACK)
  },
/*    
BarChartData:  {
        labels: [ 'January', 'February', 'March' ],
        datasets: [ { data: [40, 20, 12] } ]
      },
      BarChartOptions:  {
        type: Object,
        default: () => {}
        },
      LineChartOptions: {},
      LineChartData: {},
computed: {
      BarChartData() { return  },
      BarChartOptions() { return  },
    }
*/
}
</script>