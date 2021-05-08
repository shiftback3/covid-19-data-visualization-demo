<template>
  <CRow>
    <CCol sm="6" lg="3">
      <div class="card widget-flat bg-primary text-white">
        <div class="card-body">
          <div class="float-end">
            <i class="mdi mdi-account-multiple widget-icon"></i>
          </div>
          <h5 class="text-muted fw-normal mt-0" title="Number of Customers">
           <font-awesome-icon class="text-white" style="font-size:30px;" :icon="['fas', 'viruses']" />
          </h5>
          <h3 class="mt-3 mb-3">{{covidSatistics["New Cases_text"]}}</h3>
          <p class="mb-0 text-muted">
            
            <span class="text-nowrap text-white">New Cases</span>
          </p>
        </div>
        <!-- end card-body-->
      </div>
    </CCol>
    <CCol sm="6" lg="3">
      <div class="card widget-flat bg-warning text-white">
        <div class="card-body">
          <div class="float-end">
            <i class="mdi mdi-account-multiple widget-icon"></i>
          </div>
          <h5 class="text-muted fw-normal mt-0" title="Number of Customers">
           <font-awesome-icon class="text-white" style="font-size:30px;" :icon="['fas', 'viruses']" />
          </h5>
          <h3 class="mt-3 mb-3">{{covidSatistics["Active Cases_text"]}}</h3>
          <p class="mb-0 text-muted">
            
            <span class="text-nowrap text-white">Total Active Cases</span>
          </p>
        </div>
        <!-- end card-body-->
      </div>
    </CCol>
    <CCol sm="6" lg="3">
      <div class="card widget-flat bg-success text-white">
        <div class="card-body">
          <div class="float-end">
            <i class="mdi mdi-account-multiple widget-icon"></i>
          </div>
          <h5 class="text-muted fw-normal mt-0" title="Number of Customers">
           <font-awesome-icon class="text-white" style="font-size:30px;" :icon="['fas', 'viruses']" />
          </h5>
          <h3 class="mt-3 mb-3">{{covidSatistics["Total Recovered_text"]}}</h3>
          <p class="mb-0 text-muted">
            
            <span class="text-nowrap text-white">Total Recovered</span>
          </p>
        </div>
        <!-- end card-body-->
      </div>
    </CCol>
    <CCol sm="6" lg="3">
      <div class="card widget-flat bg-danger text-white">
        <div class="card-body">
          <div class="float-end">
            <i class="mdi mdi-account-multiple widget-icon"></i>
          </div>
          <h5 class="text-muted fw-normal mt-0" title="Number of Customers">
           <font-awesome-icon class="text-white" style="font-size:30px;" :icon="['fas', 'viruses']" />
          </h5>
          <h3 class="mt-3 mb-3">{{covidSatistics["Total Deaths_text"]}}</h3>
          <p class="mb-0 text-muted">
            
            <span class="text-nowrap text-white">Total Deaths</span>
          </p>
        </div>
        <!-- end card-body-->
      </div>
    </CCol>
    
  </CRow>
</template>

<script>
import axios from "axios";
import { CChartLineSimple, CChartBarSimple } from "../charts/index.js";

export default {
  name: "WidgetsDropdown",
  components: { CChartLineSimple, CChartBarSimple },
  data() {
    return {
      covidSatistics: {},
      options: {
        method: "GET",
        url: "https://covid-19-tracking.p.rapidapi.com/v1",
        headers: {
          "x-rapidapi-key":
            "6df9641f29msh997d4891d3c5a38p1e376bjsn45bdd2c9e825",
          "x-rapidapi-host": "covid-19-tracking.p.rapidapi.com",
        },
      },
    };
  },
  created() {
    this.LoadCovidStats();
  },
  methods: {
    LoadCovidStats() {
      axios
        .request(this.options)
        .then((data) => {
          this.active = data.data[0]["Active Cases_text"].replace(/,/g, "");
          this.recovered = data.data[0]["Total Recovered_text"].replace(
            /,/g,
            ""
          );
          this.deaths = data.data[0]["Total Deaths_text"].replace(/,/g, "");
          this.covidSatistics = data.data[0];
          console.log(this.covidSatistics);
        })
        .catch((err) => console.error(err));
    },
  },
};
</script>
