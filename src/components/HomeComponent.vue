<template>
  <div>
    <h1>{{ msg }}</h1>
    <b-container class="mt-5">
      <b-form inline>
        <label class="mr-sm-2" for="inline-form-custom-select-pref">Country</label>
        <b-form-select
          id="inline-form-custom-select-pref"
          class="mb-2 mr-sm-2 mb-sm-0"
          :options="options"
          v-model="selected"
        ></b-form-select>
        <b-button variant="primary" @click="getStats($event)">
          Get Stats
        </b-button>
      </b-form>
      <b-row class="mt-5">
        <b-col md="4" class="mt-2">
          <b-card
          >
            <b-card-body>
              <b-card-title>😔<br>Confirmed:</b-card-title>
              <b-card-sub-title class="mb-2">{{ confirmed }}</b-card-sub-title>
            </b-card-body>
          </b-card>  
        </b-col>
        <b-col md="4" class="mt-2">
          <b-card
          >
            <b-card-body>
              <b-card-title>😢<br>Deaths:</b-card-title>
              <b-card-sub-title class="mb-2">{{ deaths }}</b-card-sub-title>
            </b-card-body>
          </b-card>  
        </b-col>
        <b-col md="4" class="mt-2 mb-2">
          <b-card
          >
            <b-card-body>
              <b-card-title>😷<br>Recovered:</b-card-title>
              <b-card-sub-title class="mb-2">{{ recovered }}</b-card-sub-title>
            </b-card-body>
          </b-card>
        </b-col>
      </b-row>

      <LineChart :chartData="chartdata" :country="selected"/>
    </b-container>
  </div>
</template>

<script>
import LineChart from './LineChart';

export default {
  name: 'HomeComponent',
  components: {
    LineChart
  },
  props: ['msg'],
  data() {
    return {
      options: [],
      data: null,
      selected: "Morocco",
      confirmed: 0,
      deaths: 0,
      recovered: 0,
      chartdata: {}
    }
  },
  methods: {
    sortArray(){
        return this.options.sort((a, b) => a > b );
    },
    getStats(){
        this.chartdata = {};
        var countryStats = this.data[this.selected];
        this.confirmed =countryStats[countryStats.length-1].confirmed;
        this.deaths =countryStats[countryStats.length-1].deaths;
        this.recovered =countryStats[countryStats.length-1].recovered;
        
        var datasets = [];
        var dataset = {};
        var labels = [];
        countryStats.forEach((el)=>{
          if(!dataset.data)
            dataset.data = [];
          labels.push(el.date)
          dataset.data.push(el.confirmed);
        });
        dataset.label = "Confirmed";
        dataset.borderColor = "#3e95cd";
        dataset.fill = true;

        this.chartdata.labels = labels;
        datasets.push(dataset);
        this.chartdata.datasets = datasets;
    }
  },
  mounted () {
    this.$http
      .get('https://pomber.github.io/covid19/timeseries.json')
      .then(response => {
        this.data = response.data
        Object.keys(response.data).forEach((key)=>{
          this.options.push(key);
        })
      })
      .catch(error => {
        console.log(error)
      })
      .finally(()=>{
        this.sortArray()
      });
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
