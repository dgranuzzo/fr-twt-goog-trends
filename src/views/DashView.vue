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
                              :headers="headersGTrendsTodayHotTrends"
                              :items="itemsGTrendsTodayHotTrends"
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
                  </v-tabs>
                  </v-col>
                  </v-row>

                  <v-row>
                    <!--
                    <v-col class="d-flex" cols="12" sm="12" >
                      <BarChart 
                          ref="bar-chart" 
                          chartId="Time Variation"
                          :chartData="BarChartData"
                          :chartOptions="BarChartOptions"
                        />
                    </v-col>

                    <v-col class="d-flex" cols="12" sm="12" >
                      <line-chart
                        :chart-options='LineChartOptions'
                        :chart-data='LineChartData'
                        chart-id='myCustomId'
                        ref="line-chart"
                      />
                    </v-col>
                    -->
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
        <v-card-title class="headline">Pesqisando...</v-card-title>
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
//import BarChart from '@/components/BarChart.vue'
//import LineChart from '@/components/LineChart.vue'

const headers = {
    'Content-Type': 'application/json',
    'Access-Control-Allow-Headers': '*',
    'Access-Control-Allow-Origin':'*'
}
const URL_BACK= process.env.VUE_APP_URL_BACK

export default {
  name: 'DashView',
  components: {

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
      
      headersGTrendsTodayHotTrends: [
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
      itemsGTrendsTodayHotTrends: [],

      headersGTrendsRealTimeSearch:[
        {
          text:'Título',
          align:'start',
          sortable: false,
          value:'results',
        },
      ],
      itemsGTrendsRealTimeSearch: [],
      
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
              text: 'Query',
              align: 'start',
              sortable: false,
              value: 'query',
            },                        
            {
              text: 'Data',
              align: 'start',
              sortable: false,
              value: 'timestamp',
            }, 
      ],
      itemsTwitterTrends:[],
       
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
      //let url = this.URL_BACK + "gt_realtime"?query=" + this.location
      let url = URL_BACK + "gt_hot?query=" + this.searchString
      console.log(url)
      let vueInstance = this
      axios.get(url, {
           headers: headers
         }).then(response => {
           console.log(response)
           vueInstance.performingRequest = false
           vueInstance.itemsGTrendsTodayHotTrends = response.data.results.results
           console.log(vueInstance.itemsGNews)
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
      let vueInstance = this
      axios.get(url, {
           headers: headers
         }).then(response => {
           console.log(response)
           vueInstance.performingRequest = false
           vueInstance.itemsTwitter = response.data.results
           vueInstance.itemsTwitterTrends = response.data.trends
           
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

  },
  created() {
    console.log(process.env.BASE_URL)
    console.log(URL_BACK)
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