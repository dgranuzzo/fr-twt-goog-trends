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
                  <v-row
                    class="pa-2"
                    justify="center"
                    align="center"
                  >
                     <v-col class="d-flex" cols="4" sm="4" >
                     </v-col>
                    <v-col class="d-flex" cols="4" sm="4" >
                    <v-btn
                      color="primary"
                      @click="searchData()"
                    >
                      Pesquisar
                    </v-btn>
                    </v-col>
                     <v-col class="d-flex" cols="4" sm="4" >
                     </v-col>
                  </v-row>                  

                  <!-- CHARTS -------- -->
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                        <v-col class="d-flex" cols="6" sm="12" >
                          <BarChart 
                              ref="bar-chart" 
                              chartId="bar-chart-1"
                              :chartData="twitterTrendsBarChartData"
                              :chartOptions="BarChartOptions"
                              title="Twitter Trends"
                              :msg="twitterTrendsMsg"
                            />
                        </v-col>
                      </v-row>
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >

                        <v-col class="d-flex" cols="6" sm="6" >
                          <DoghnutChart
                           title="Likes x Retweets"
                            :chartOptions='DoughChartOptions'
                            :chartData='tweetRetFavDoghnut'
                            chart-id='myDog1'
                            ref="dog-chart"
                          />
                        </v-col>
                        <v-col class="d-flex" cols="6" sm="6" >
                          <BarChart
                           title="Likes x retweets"
                            :chartOptions='BarChartOptions'
                            :chartData='twitterBarChartData'
                            chart-id='myscatter-1'
                            ref="scatt-chart"
                          />
                        </v-col>
                      </v-row>                        
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                        <v-col class="d-flex" cols="6" sm="12" >
                              <BarChart 
                                  ref="bar-chart" 
                                  chartId="time-Variation"
                                  :chartData="googleTrendsBarChartData"
                                  :chartOptions="BarChartOptions"
                                  :height="heightChart"
                                  :msg="googleTrendsMsg"
                                  title="Google Trends Interest Over Time"
                                />
                        </v-col>
                      </v-row>                        
                      <v-row
                        class="pa-2"
                        justify="center"
                        align="center"
                      >
                      <v-col class="d-flex" cols="12" sm="12" >
                        <v-container fluid>
                        <v-card
                          class="mx-auto"
                          elevation="2"
                          fluid                          
                        >
                        <v-card-title> Google News Data</v-card-title>
                            <v-data-table
                              :headers="headersGNews"
                              :items="itemsGNews"
                              :items-per-page="5"
                              class="elevation-1"
                            ></v-data-table>
                          <!--
                          <LineChart
                            title="Line test"
                            :chartOptions='LineChartOptions'
                            :chartData='LineChartData'
                            chart-id='line-1-Id'
                            ref="line-chart"
                          />
                          -->
                        
                        </v-card>
                        </v-container>  
                      </v-col>
                      </v-row>
                      
                      <v-row
                          class="pa-2"
                          justify="center"
                          align="center"
                         >
                        <v-col class="d-flex" cols="12" sm="12" >
                        <v-container fluid>
                        <v-card
                          class="mx-auto"
                          elevation="2"
                          fluid                          
                        >
                        <v-card-title> Google Trends Data</v-card-title>

                            <v-data-table
                              :headers="headersGTrendsTodayHot"
                              :items="itemsGTrendsTodayHot"
                              :items-per-page="10"
                              class="elevation-1"
                            ></v-data-table>
                        </v-card>
                        </v-container>
                           </v-col>
                      </v-row>
                      
                      <!-- Tables Twitter -->
                      <v-row
                          class="pa-2"
                          justify="center"
                          align="center"
                         >
                        <v-col class="d-flex" cols="12" sm="12" >
                        <v-container fluid>
                        <v-card
                          class="mx-auto"
                          elevation="2"
                          fluid                          
                        >
                        <v-card-title> Twitter Data</v-card-title>
                            <v-data-table
                              :headers="headersTwitter"
                              :items="itemsTwitter"
                              :items-per-page="10"
                              class="elevation-1"
                            ></v-data-table>
                        <v-divider></v-divider>
                            <v-data-table
                              :headers="headersTwitterTrends"
                              :items="itemsTwitterTrends"
                              :items-per-page="10"
                              class="elevation-1"
                            ></v-data-table>

                        </v-card>
                        </v-container>
                        </v-col>
                      </v-row>
            
                 <v-row
                    class="pa-2"
                    justify="center"
                    align="center"
                  >
                    <v-col class="d-flex" cols="12" sm="12" >
                    {{ errorMsg }}
                    </v-col>
                  </v-row>
      </v-card>
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
// https://vue-chartjs.org/examples/
//import HelloWorld from '@/components/HelloWorld.vue'
import axios from 'axios'
import BarChart from '@/components/BarChart.vue'
//import LineChart from '@/components/LineChart.vue'
import DoghnutChart from '@/components/DoghnutChart.vue'
//import ScatterChart from '@/components/ScatterChart.vue'

const headers = {
    'Content-Type': 'application/json',
    'Access-Control-Allow-Headers': '*',
    'Access-Control-Allow-Origin':'*'
}
const URL_BACK= process.env.VUE_APP_URL_BACK

const chartOptions= {
        responsive: true,
        maintainAspectRatio: false,
}

const doughnutChartOptions= {
        responsive: true,
        maintainAspectRatio: false,
        scales: {
          x: {
              grid: {
                  display:false
              }
          },
          y: {
              grid: {
                  display:false,
              }   
          }
        }

}

export default {
  name: 'DashView',
  components: {
    BarChart,
    //LineChart,
    DoghnutChart,
    //ScatterChart,
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
      
      googleTrendsMsg: "",
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

      twitterTrendsMsg:"",
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

      twitterScatterChartData: {},
      tweetRetFavDoghnut:{},
      tweetRetFavXY:[],
      twitterBarChartData: {},
 
      ScatterChartOptions:chartOptions,
      DoughChartOptions:doughnutChartOptions,
      BarChartOptions: chartOptions,
      LineChartOptions: chartOptions,
      
      LineChartData:{
        labels: [ 'Jan', 'Feb', 'Mar'],
        datasets: [
          {
             label: 'Data chart',
             backgroundColor: 'rgb(75, 192, 192)',
             borderColor: 'rgb(75, 192, 192)',
             borderJoinStyle: 'bevel',
            tension:0.1,
            data: [40, 20, 12]
          }
        ]
      }, 
        

      //favoriteCountArray: [],
      //retweetCountArray: [],

      twitterTrendsBarChartData: {},
      //twitterTrendsBarChartDataSet: [],
      //twitterTrendsBarChartLabels: [],
      heightChart: 1800,
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
          
           if (response.data.today_hot_trends.status) {
             vueInst.itemsGTrendsTodayHot = response.data.today_hot_trends.results
           } else {
             vueInst.googleTrendsMsg = response.data.today_hot_trends.results
           }
           
           if (response.data.realtime_searches.status == 'ok') {
            vueInst.itemsGTrendsRealTimeSearch = response.data.realtime_searches.results
           } else {
            vueInst.googleTrendsMsg = response.data.realtime_searches.results
           }
                      
           if (response.data.int_over_time.status == "ok") {
            vueInst.itemsGTrendsInterestTime = response.data.int_over_time.results
            let nodes = vueInst.itemsGTrendsInterestTime[vueInst.searchString]

            let dataLabels = []
            let dataSet = []
            Object.entries(nodes).forEach(([key, value]) => {
              //console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
              dataLabels.push(key.toString().slice(0,10))
              dataSet.push(value)
            })
            vueInst.googleTrendsBarChartData = this.createChartDataObj(dataLabels, dataSet, vueInst.searchString, '#f87979')
           } else {
            console.log('error else gTrends')
            vueInst.errorMsg = "Interest Over Time" + response.data.int_over_time.results
            vueInst.googleTrendsMsg = "Interest Over Time" + response.data.int_over_time.results
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
           if (response.data.response == 'ok') {
             vueInst.itemsTwitter = response.data.results

             let nodes = response.data.results
             let tweetRetFav = nodes.map((node) => 
                [node.favorite_count,node.retweet_count]
              )

             let tweetRetweets = nodes.map((node) => node.retweet_count)
             let tweetFavorites = nodes.map((node) => node.favorite_count)
             let tweetNames = nodes.map((node) => node.user.name)

             let tweetRetFavXY = []
             let retweetCount = 0
             let favoriteCount = 0
             // tweetRetFavXY is array p/ scatter
            Object.entries(tweetRetFav).forEach((item) => {
              //console.log(`${key} ${value}`); // "a 5", "b 7", "c 9"
              
              let varX = 0
              if (isNaN(item[1][0])) {
                varX = 0
              } else {
                 varX = item[1][0]
              } 

              let varY = 0   
              if (isNaN(item[1][1])) {
                 varY = 0
              } else {
                 varY = item[1][1]      
              } 

              retweetCount += varX
              favoriteCount += varY

              tweetRetFavXY.push({
                'x':varX,
                'y':varY
              })
            })
            
            vueInst.twitterBarChartData = {
              labels: tweetNames, 
              datasets: [
                {
                  label: 'Favorites',
                  backgroundColor: '#115579',
                  data: tweetFavorites
                },
                {
                  label: 'Retweets',
                  backgroundColor: '#f87979',
                  data: tweetRetweets
                },
              ]
            },
            
            this.createChartDataObj(
                  ['Favorites','Retweets'], 
                  tweetRetFavXY, 
                  'Favorites x Retweets',
                  '#f87979')              
            
            console.log('tweet-retweet-favorites:')
            console.log(tweetRetFavXY)
            console.log('=====----====')

            /*
            let retweetCountArray = nodes.map((node) => node.retweet_count);
            console.log(retweetCountArray)
            // soma valores do array
            let retweetCount = retweetCountArray.reduce(
              (previousValue, currentValue) => previousValue + currentValue,
            )

            let favoriteCountArray = nodes.map((node) => node.favorite_count);            
            console.log(favoriteCountArray)
            let favoriteCount = favoriteCountArray.reduce(
              (previousValue, currentValue) => previousValue + currentValue,
            )
            */
            let dataLabelsDog = ['Retweet','Favorite']
            let dataSetDog = [retweetCount, favoriteCount]
            let colorInfo = ['rgb(75, 192, 192)','rgb(75, 75, 192)']
            console.log(dataSetDog)
            vueInst.tweetRetFavDoghnut = this.createChartDataObj(dataLabelsDog, dataSetDog, 'Favorites x Retweets',colorInfo)
            console.log('end twitter info')

            // TWITTER TRENDS
            vueInst.itemsTwitterTrends = response.data.trends
            nodes = response.data.trends
             /* Map each item of nodes to a nested array where each is a row of two columns */
            let dataLabels = nodes.map((node) => node.name);
            let dataSet = nodes.map((node) => node.tweet_volume);
            vueInst.twitterTrendsBarChartData = this.createChartDataObj(dataLabels, dataSet, 'Tweets volume', 'rgb(75, 192, 192)')
            

           } else {
            vueInst.twitterTrendsMsg = "Twitter Search" + response.data.results
            console.log('else twitter')
           }
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

    createChartDataObj(labelsArr, dataArr, label, color,) {
      let ChartData= {
        labels: labelsArr,
        datasets: [
          {
            label: label,
            backgroundColor: color, //'rgb(75, 192, 192)',
            borderColor: color, //'rgb(75, 192, 192)',
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
      DogChartData: {labels: [ 'Jan', 'Feb', 'Mar'],
        datasets: [
          {
            label: 'Data One',
            backgroundColor: ['#f87979','#0033aa','#456600'],
            data: [40, 20, 12]
          }
        ]},
     twitterLikexRetweetChartData: {
       datasets: [
        {
          label: 'Scatter Dataset 1',
          fill: false,
          borderColor: '#f87979',
          backgroundColor: '#f87979',
          data: [
            {x: 10,y:15},
            {x: 12,y:16},
            {x: 15,y:13},
            {x: 17,y:21},
            ]
          }
       ],
      },      
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
      

computed: {
      BarChartData() { return  },
      BarChartOptions() { return  },
    }
*/
}
</script>