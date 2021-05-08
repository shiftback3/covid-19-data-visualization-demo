<template>
  <CChartDoughnut
    :datasets="defaultDatasets"
    :labels="['Active', 'Recovered', 'Deaths']"
  />
</template>

<script>
import { CChartDoughnut } from '@coreui/vue-chartjs'
import axios from "axios";
// const options = {
//     method: 'GET',
//     url: 'https://covid-19-tracking.p.rapidapi.com/v1',
//     headers: {
//       'x-rapidapi-key': '6df9641f29msh997d4891d3c5a38p1e376bjsn45bdd2c9e825',
//       'x-rapidapi-host': 'covid-19-tracking.p.rapidapi.com'
//     }
//   };

export default {
  name: 'CChartDoughnutExample',
  components: { CChartDoughnut },
  data(){
    return{
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
  //  this.data = [6,8,3]
  },
  methods:{
    LoadCovidStats(){
 axios.request(this.options).then(data => {
          this.active = data.data[0]["Active Cases_text"].replace(/,/g, "");
			this.recovered = data.data[0]["Total Recovered_text"].replace(/,/g, "");
			this.deaths = data.data[0]["Total Deaths_text"].replace(/,/g, "");
      this.data = [this.active,this.recovered,this.deaths]
          console.log(this.data)
        })
        .catch(err => console.error(err));
  
  // this.data = this.active
   
// this.data = [60, 20, 80, 10]
    }

  },
  computed: {
    defaultDatasets () {
      return [
        {
          backgroundColor: [
            '#41B883',
            '#E46651',
            '#00D8FF',
            '#DD1B16'
          ],
          data: this.data
        }
      ]
    }
  }
}
</script>
