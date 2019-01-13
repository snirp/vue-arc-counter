<template>
  <div id="app">
    <div>
      <ArcCounter width="10rem" height="10rem" :start="-40" :end="40"></ArcCounter>
      <table class="prop-table">
        <thead>
          <tr><th>Property</th><th>Value</th></tr>
        </thead>
        <tbody>
        <tr><td>width</td><td>10rem</td></tr>
        <tr><td>height</td><td>10rem</td></tr>
        <tr><td>dashCount</td><td>21</td></tr>
        <tr><td>activeCount</td><td>5</td></tr>
        <tr><td>strokeWidth</td><td>20</td></tr>
        <tr><td>stroke</td><td>lightgrey</td></tr>
        <tr><td>activeStroke</td><td>dodgerblue</td></tr>
        <tr><td>dashSpacing</td><td>1/4</td></tr>
        <tr><td>start</td><td>-40</td></tr>
        <tr><td>end</td><td>40</td></tr>
        </tbody>
      </table>
    </div>
    <div>
      <ArcCounter width="10rem" height="10rem" :strokeWidth="60" :dashCount="45" :activeCount="17" :dashSpacing="0.6" :start="300" :end="60"></ArcCounter>
      <table class="prop-table">
        <thead>
          <tr><th>Property</th><th>Value</th></tr>
        </thead>
        <tbody>
        <tr><td>width</td><td>10rem</td></tr>
        <tr><td>height</td><td>10rem</td></tr>
        <tr><td>dashCount</td><td>45</td></tr>
        <tr><td>activeCount</td><td>17</td></tr>
        <tr><td>strokeWidth</td><td>60</td></tr>
        <tr><td>stroke</td><td>lightgrey</td></tr>
        <tr><td>activeStroke</td><td>dodgerblue</td></tr>
        <tr><td>dashSpacing</td><td>0.6</td></tr>
        <tr><td>start</td><td>300</td></tr>
        <tr><td>end</td><td>60</td></tr>
        </tbody>
      </table>
    </div>
    <div>
      <ArcCounter width="10rem" height="10rem" :start="140" :end="-140" :strokeWidth="3" stroke="darkgrey" activeStroke="red" :dashSpacing="1/10"></ArcCounter>
      <table class="prop-table">
        <thead>
          <tr><th>Property</th><th>Value</th></tr>
        </thead>
        <tbody>
        <tr><td>width</td><td>10rem</td></tr>
        <tr><td>height</td><td>10rem</td></tr>
        <tr><td>dashCount</td><td>21</td></tr>
        <tr><td>activeCount</td><td>5</td></tr>
        <tr><td>strokeWidth</td><td>3</td></tr>
        <tr><td>stroke</td><td>darkgrey</td></tr>
        <tr><td>activeStroke</td><td>red</td></tr>
        <tr><td>dashSpacing</td><td>1/10</td></tr>
        <tr><td>start</td><td>140</td></tr>
        <tr><td>end</td><td>-140</td></tr>
        </tbody>
      </table>
    </div>

    
  </div>
</template>

<script>
import ArcCounter from '@/ArcCounter.vue'

export default {
  name: 'app',
  components: {
    ArcCounter
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  justify-content: space-around;
}

.prop-table {
  margin-top: 4rem;
}

.prop-table td, .prop-table th {
  padding: 0 1rem;
}

.prop-table tr td:nth-child(1), .prop-table tr th:nth-child(1){
  text-align: left;
}
.prop-table tr td:nth-child(2), .prop-table tr th:nth-child(2){
  text-align: right;
}
</style>
