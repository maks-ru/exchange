<template>
  <div id="app">
    <stock />
    <!-- <el-table :data="tableData" border style="width: 600px">
      <el-table-column prop="price" label="Цена" width="180" />
      <el-table-column prop="quantity" label="Количество" width="180" />
      <el-table-column prop="all" label="Всего" />
    </el-table>
    Currency
    {{ Price }} -->
  </div>
</template>

<script>
import Stock from '@/components/Stock.vue'
export default {
  components: {
    Stock,
  },
  name: 'App',
  data: function () {
    return {}
  },
}

// {"e":"trade","E":1685117909729,"s":"BTCUSDT","t":3126996887,"p":"26776.95000000","q":"0.01824000","b":21257069432,"a":21257071479,"T":1685117909729,"m":true,"M":true}

//////////////////////////
// {"e":"24hrTicker","E":1685114224971,"s":"ETHEUR","p":"39.39000000","P":"2.346","w":"1692.63860911","x":"1678.66000000","c":"1718.10000000","Q":"0.10720000","b":"1717.90000000","B":"0.02240000","a":"1718.09000000","A":"0.02420000","o":"1678.71000000","h":"1719.23000000","l":"1669.16000000","v":"7898.77170000","q":"13369765.94397600","O":1685027824970,"C":1685114224970,"F":87600757,"L":87638916,"n":38160}

// ws: new WebSocket('wss://stream.binance.com:9443/ws/etheur@trade'),
// ws: new WebSocket('wss://stream.binance.com:9443/ws/bnbbtc@depth'),
// ws: new WebSocket('wss://stream.binance.com:9443/ws/ethbtc@ticker'),

// {"e":"trade","E":1685110160248,"s":"ETHEUR","t":87634471,"p":"1705.67000000","q":"0.10000000","b":2301543768,"a":2301543752,"T":1685110160247,"m":false,"M":true}

// {"e":"24hrTicker","E":1685111885892,"s":"ETHBTC","p":"0.00009000","P":"0.132","w":"0.06850389","x":"0.06820000","c":"0.06828000","Q":"0.45440000","b":"0.06827000","B":"53.92680000","a":"0.06828000","A":"37.63240000","o":"0.06819000","h":"0.06880000","l":"0.06808000","v":"53642.53300000","q":"3674.72222652","O":1685025485891,"C":1685111885891,"F":418494000,"L":418569523,"n":75524}

// {"e":"depthUpdate","E":1685112073066,"s":"BNBBTC","U":3060913973,"u":3060913976,"b":[["0.01146900","15.91400000"],["0.01146600","8.92600000"]],"a":[["0.01147800","4.15800000"],["0.01153400","0.59700000"]]}
</script>

<style>
body {
  background: rgb(94, 102, 115);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
