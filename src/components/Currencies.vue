<template>
<div id="Currencies">
  <div v-for="symbol in currenciesFormatted" v-bind:key="symbol.symbol">{{symbol.symbol}} {{symbol.currentValue}} {{symbol.change}}</div>
</div>
</template>

<script>
// import { BModal, BFormInput, BContainer, BTab, BTabs } from 'bootstrap-vue'
import axios from 'axios';
export default {
  data:
  function () {
    return {
      currenciesList: ['EUR', 'USD', 'CHF'],
      currenciesRaw: [],
      currenciesFormatted: []
    }
  },
  name: 'Currencies',
  mounted: function () {
        this.$nextTick(function () {
            window.setInterval(() => {
                this.getCurrencies()
            },1000);
        })
  },
  watch: {
    currenciesRaw: function () {
      this.createCurrenciesData()
    }
  },
  methods: {
    getCurrencies: function () {
      axios.get('http://api.nbp.pl/api/exchangerates/tables/a/last/2?format=JSON').then(r =>
        this.currenciesRaw = r.data)
    },
    createCurrenciesData: function () {
      this.currenciesFormatted = []
      this.currenciesList.forEach(currency => this.getDataforSymbol(currency))
    },
    getDataforSymbol: function (symbol) {
      const previousValue = this.currenciesRaw[0].rates.find(x => x.code === symbol).mid
      const currentValue = this.currenciesRaw[1].rates.find(x => x.code === symbol).mid
      const change = ((currentValue/previousValue - 1) * 100).toFixed(2)
      const symbolObject = {
        symbol: symbol,
        currentValue: currentValue,
        change: change
      }
      this.currenciesFormatted.push(symbolObject)
    }
  }
}
</script>

