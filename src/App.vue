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
      <div class="tab-pane" id="covid19"><p><img src="https://1.bp.blogspot.com/-40pTEBTtP30/XAA8Yz8FBxI/AAAAAAAAdjU/a2J2178s9asP-83xYl0bGgWZEIlbq0ZqACLcBGAs/s1600/Work-in-progress-1024x603.png"></p></div>
    </div>
  </div>
</template> 

<script> 
import Currencies from './components/Currencies.vue'
import 'bootstrap'
import 'bootstrap/dist/css/bootstrap.min.css'
import 'moment'
export default {
  name: 'App',
  components: {
    Currencies
  }
}
</script>
