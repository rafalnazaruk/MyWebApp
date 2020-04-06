<template>
  <div id="app">
    <ul class="nav nav-tabs">
      <li class="nav-item">
        <a class="nav-link active" href=#currencies role="tab" data-toggle="tab">Kursy walut</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href=#covid19 role="tab" data-toggle="tab">COVID-19</a>
      </li>
    </ul>
    <div class="tab-content">
      <div class="tab-pane active" id="currencies"><Currencies/></div>
      <div class="tab-pane" id="covid19"><p>WORK IN PROGRESS</p></div>
    </div>
  </div>
</template> 

<script> 
import Currencies from './components/Currencies.vue'
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'
export default {
  name: 'App',
  components: {
    Currencies
  }
}
</script>
