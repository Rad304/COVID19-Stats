<script>
import { Line, mixins } from 'vue-chartjs'
const { reactiveProp } = mixins

export default {
  name: 'LineChart',
  extends: Line,
  mixins: [reactiveProp],
  props: ["country"],
  data(){
      return {     
        options: {
            title: {
            display: true,
            text: 'Coronavirus statistics in ' + this.country
            },
        }
      } 
  },
  mounted () {
    this.renderChart(this.chartData, this.options)
  },
  
}
</script>

<style>
</style>
