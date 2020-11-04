<template>
  <section>
    <table class="crypto-list">
      <thead class="crypto-list__head">
        <tr class="crypto-list__head-item">
          <th class="crypto-list__head-item-value">#</th>
          <th class="crypto-list__head-item-value">Name</th>
          <th class="crypto-list__head-item-value">Market Cap</th>
          <th class="crypto-list__head-item-value">Price</th>
          <th class="crypto-list__head-item-value">Open (24h)</th>
        </tr>
      </thead>

      <tbody>
        <tr
          class="crypto-list__body-item"
          v-for="(value, key, index) in coins" v-bind:key="key.id"
          @click="showChart(key)"
        >
          <th>{{index+1}}</th>
          <td class="crypto-list__body-item-value">{{key}}</td>
          <td class="crypto-list__body-item-value">{{value.USD.MKTCAP}}</td>
          <td class="crypto-list__body-item-value">{{value.USD.PRICE}}</td>
          <td class="crypto-list__body-item-value">{{value.USD.OPEN24HOUR}}</td>
        </tr>
      </tbody>

      <tfoot class="crypto-list__head">
        <tr>
          <th class="crypto-list__head-item-value">#</th>
          <th class="crypto-list__head-item-value">Name</th>
          <th class="crypto-list__head-item-value">Market Cap</th>
          <th class="crypto-list__head-item-value">Price</th>
          <th class="crypto-list__head-item-value">Open (24h)</th>
        </tr>
      </tfoot>
    </table>

    <CryptoChart
      :coin="coinToShow"
      v-if="chartVisibility"
    />
  </section>
</template>

<script>
  import axios from 'axios';
  import CryptoChart from "./CryptoChart";

  export default {
    data() {
      return {
          coins: [],
          coinToShow: '',
          chartVisibility: false
        }
      },

    components: {
      CryptoChart
    },
      
    created() {
      axios.get('https://min-api.cryptocompare.com/data/pricemultifull?fsyms=BTC,ETH,USDT,XRP,BCH,LINK,BNB,LTC,DOT,BSV,USDC,ADA,EOS,XMR,TRX&tsyms=USD,EUR')
        .then(response => {
        this.coins = response.data.DISPLAY;
      });
    },

    methods: {
      showChart(key) {
        this.chartVisibility = true;
        this.coinToShow = key;
      }
    }
  }
</script>

<style lang="scss" scoped>
  .crypto-list {
    width: 45%;
    border: 1px solid #789Fbb;
    background-color: #cddce7;

    &__head {
      background-color: #789Fbb;
    }

    &__head-item-value {
      padding: 10px;
    }

    &__body-item {
      &:hover {
        background-color: #fff;
        cursor: pointer;
      }
    }

    &__body-item-value {
      padding: 5px;
    }
  }
</style>
