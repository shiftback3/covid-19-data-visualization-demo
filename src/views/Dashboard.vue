<template>
  <div>
   
   <CRow>
      <CCol sm="12" lg="12">
        <CWidgetProgress footer="">
          <div class="h4 m-0 p-3" style="background-color:grey; width:min-content; border-radius:5px;">{{covidSatistics["Total Cases_text"]}}</div>
          <div class="card-header-actions">
            
              <!-- <small class="text-muted">docs</small> -->
            
          </div>
          <div style="font-size:18px; font-weight:bolder ">Total Cases</div>
         <div>Last updated: {{covidSatistics['Last Update']}}</div>
        </CWidgetProgress>
      </CCol>
   </CRow>
    <WidgetsDropdown/>
    <CCard>
      <CCardBody>
        <CRow>
          <CCol sm="5">
            <h4 id="traffic" class="card-title mb-0">Covid-19 Statistics</h4>
            <!-- <div class="small text-muted">November 2017</div> -->
          </CCol>
          <CCol sm="7" class="d-none d-md-block">
            
          </CCol>
        </CRow>
         <CChartDoughnut
         
    :datasets="defaultDatasets"
    :labels="['Active', 'Recovered', 'Deaths']"
  />
        <!-- <CChartDoughnutExample style="height:300px;margin-top:40px;"/> -->
        <!-- <MainChartExample style="height:300px;margin-top:40px;"/> -->
      </CCardBody>
      
        </CCard>
       
  </div>
</template>

<script>
import MainChartExample from './charts/MainChartExample'
import WidgetsDropdown from './widgets/WidgetsDropdown'
import WidgetsBrand from './widgets/WidgetsBrand'
import axios from "axios";

import { CChartDoughnut } from '@coreui/vue-chartjs'

export default {
  name: 'Dashboard',
  components: {
    CChartDoughnut,
    MainChartExample,
    WidgetsDropdown,
    WidgetsBrand,
    
  },
  data () {
    return {
      covidSatistics:{},
        options:{
    method: 'GET',
    url: 'https://covid-19-tracking.p.rapidapi.com/v1',
    headers: {
      'x-rapidapi-key': '6df9641f29msh997d4891d3c5a38p1e376bjsn45bdd2c9e825',
      'x-rapidapi-host': 'covid-19-tracking.p.rapidapi.com'
    }
  },
  data:[],
      // dataa:[],
      active:'',
      recovered:'',
      deaths:''

    }
  },
  created(){
this.LoadCovidStats()
  },
  methods: {
       LoadCovidStats(){
 axios.request(this.options).then(data => {
          this.active = data.data[0]["Active Cases_text"].replace(/,/g, "");
			this.recovered = data.data[0]["Total Recovered_text"].replace(/,/g, "");
			this.deaths = data.data[0]["Total Deaths_text"].replace(/,/g, "");
     this.covidSatistics = data.data[0]
      this.data = [this.active,this.recovered,this.deaths]
          console.log(this.covidSatistics)
        })
        .catch(err => console.error(err));
  
     }
   
  },
   computed: {
    defaultDatasets () {
      return [
        {
          backgroundColor: [
            "#FFCE51",							
							"#20D077",
							"#EF6262"
          ],
          data: this.data
        }
      ]
    }
  }
}
</script>
