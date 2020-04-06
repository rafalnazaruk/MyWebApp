<template>
<div id="Currencies">
    <div v-for="symbol in currenciesFormatted"
         v-bind:key="symbol.symbol"
         class="card">
      <div class="card-header">
        <strong>{{symbol.symbol}}</strong>
      </div>
      <ul class="list-group list-group-flush">
        <li class="list-group-item">
          <strong>{{symbol.currentValue}}</strong>
        </li>
        <li class="list-group-item">
          <strong :class="(symbol.change >= 0) ? 'green' : 'red'">{{symbol.change}}</strong>
        </li>
      </ul>
    </div>
</div>
</template>

<script>
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'
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
<style scoped>
.card {
  display: inline-block;
  text-align: center;
  vertical-align: middle;
  width: 6rem;
  margin-top: 25px;
  margin-left: 25px;
}
.card-header, .list-group-item {
  height: 3rem;
}
strong.green {
  color: green;
}
strong.red {
  color: red;
}
</style>