<template>
  <div class="container">
    <line-chart
      :chart-data="data"
      class="chart"
    />
  </div>
</template>

<script>
  import LineChart from './LineChart.js';
  import axios from 'axios';

  export default {
    props: {
      coin: String
    },

    components: {
      LineChart
    },

    data() {
      return {
        coinPrices: [],
        data: null,
        loaded: false
      }
    },

    mounted() {
      this.update();
      this.loaded = true;
    },

    updated() {
      this.update();
    },

    methods: {
      update() {
        axios.get('https://min-api.cryptocompare.com/data/v2/histoday?fsym=' + this.coin + '&tsym=USD&limit=10')
          .then(response => {
            this.coinPrices = response.data.Data.Data.map(element => element.close)

            this.data = {
              labels: ['', '', '', '', '', '', '', '', '', '', ''],
              datasets: [
                {
                  label: this.coin + ' price for 24 hours',
                  data: this.coinPrices,
                  backgroundColor: "transparent",
                  borderColor: "rgba(1, 116, 188, 0.50)",
                  pointBackgroundColor: "rgba(171, 71, 188, 1)"
                }
              ]
            }
          })
      }
    }
  }
</script>

<style lang="scss" scoped>
  .container {
    width: 50%;
    margin: 40px 140px;
    max-width: 600px;
    max-height: 400px;

    position: absolute;
    top: 0;
    right: 0;
  }

  .chart {
    border: 1px solid #789fbb;
    background-color: #cddce7;
  }
</style>
