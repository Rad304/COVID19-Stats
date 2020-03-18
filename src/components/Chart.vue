<script>
import { Line } from 'vue-chartjs'

export default {
  extends: Line,
  props: {
      'countries': Object, 
      'selected': String
  },
  data(){
      return {
          
        datacollection: {
          //Data to be represented on x-axis
          labels: this.selected,
          datasets: [
            {
              label: 'Data One',
              backgroundColor: '#f87979',
              pointBackgroundColor: 'white',
              borderWidth: 1,
              pointBorderColor: '#249EBF',
              //Data to be represented on y-axis
              data: [40, 20, 30, 50, 90, 10, 20, 40, 50, 70, 90, 100]
            }
          ]
        },
        //Chart.js options that controls the appearance of the chart
        options: {
          scales: {
            yAxes: [{
              ticks: {
                beginAtZero: true
              },
              gridLines: {
                display: true
              }
            }],
            xAxes: [ {
              gridLines: {
                display: false
              }
            }]
          },
          legend: {
            display: true
          },
          responsive: true,
          maintainAspectRatio: false
        }
      }
    },
  methods: {
      getLabels : ()=>{
          var labels = [];
          this.data[this.selected].array.forEach(element => {
              labels.push(element.date);
          });
          console.log(labels);
          return labels;
      }
  },
  mounted () {
    this.renderChart(this.datacollection, this.options)
  }
}
</script>

<style>

</style>