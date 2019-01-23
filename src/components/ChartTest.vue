<script>
  import VueCharts from 'vue-chartjs'
  import {Line, mixins} from 'vue-chartjs'
  export default {
    mixins: [Line, mixins.reactiveData],
    data: function() {
      return {
        options: {},
      }
    },
    props: {
      data: {
        type: Array,
        required: true,
      },
      labels: {
        type: Array,
        required: true,
      },
    },
    watch: {
      data: function() {
        this.updateChartData()
      },
    },
    methods: {
      updateChartData() {
        const newChartData = Object.assign({}, this.chartData)
        newChartData.datasets[0].data = [this.data]
        this.chartData = newChartData
      },
    },
    mounted: function() {
      this.chartData = {
        labels: [this.labels],
        datasets: [{
          label: 'data',
          data: [this.data],
        }],
        options: {
          scales: {
            yAxes: [{
              tickes: {
                beginAtZero: true
              }
            }]
          }
        }
      }
    }
  }
</script>
