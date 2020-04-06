<template>
<div id="Currencies">
  <div>Test</div>
  <div>USD: {{this.usd}} PLN</div>
  <div>EUR: {{this.eur}} PLN</div>
  <div>random value: {{this.random}}</div>
</div>
</template>

<script>
// import { BModal, BFormInput, BContainer, BTab, BTabs } from 'bootstrap-vue'
import axios from 'axios';
export default {
  data:
  function () {
    return {
      usd: '',
      eur: '',
      random: ''
    }
  },
  name: 'Currencies',
  mounted: function () {
        this.$nextTick(function () {
            window.setInterval(() => {
                this.getCurrencies();
            },1000);
        })
  },
  methods: {
    getCurrencies: function () {
      axios.get('http://api.nbp.pl/api/exchangerates/rates/A/USD?format=JSON').then(r => {
        this.usd = r.data.rates[0].mid
      }
      )
      axios.get('http://api.nbp.pl/api/exchangerates/rates/A/EUR?format=JSON').then(r => {
        this.eur = r.data.rates[0].mid
      }
      )
      axios.get('https://randomuser.me/api/').then(r => {
        this.random = r.data.results[0].name.first
      }
      )
    }
  }
}
</script>

