<template>
  <table>
    <tr>
      <th>Цена(USDT)</th>
      <th>Количество(BTC)</th>
    </tr>
    <tr v-for="ask in asks" :key="ask">
      <td class="ask">
        {{ ask[0] }}
      </td>
      <td>
        {{ ask[1] }}
      </td>
    </tr>
    <tr>
      <th :style="styleObject">{{ Price }}</th>
      <th>spread: {{ spreadPrice }} %</th>
    </tr>
    <tr v-for="bid in bids" :key="bid">
      <td class="bid">
        {{ bid[0] }}
      </td>
      <td>
        {{ bid[1] }}
      </td>
    </tr>
  </table>

</template>

<script>
import axios from 'axios';

export default {
  name: 'Stock',
  data: function () {
    return {
      price: new WebSocket(
          'wss://stream.binance.com:9443/stream?streams=bnbusdt@trade'
      ),
      ws: new WebSocket(
          'wss://stream.binance.com:9443/ws/bnbusdt@depth10@100ms'
      ),
      spread: new WebSocket(
          'wss://stream.binance.com:9443/stream?streams=bnbusdt@ticker'
      ),
      asks: [],
      bids: [],
      spreadPrice: null,
      Price: null,
      styleObject: {}
    };
  },

  computed: {},
  created: function () {
    this.ws.onmessage = event => {
      let stockObject = JSON.parse(event.data);
      this.asks = stockObject.asks;
      this.bids = stockObject.bids;
    };
    this.ws.error = error => {
      console.log(error);
    };

    this.price.onmessage = event => {
      let stockObject = JSON.parse(event.data);
      let price = parseFloat(stockObject.data.p).toFixed(1);
      this.styleObject = !this.Price || this.Price === price
          ? {color: '#fff'}
          : price > this.Price
              ? {color: '#0ECB81'}
              : {color: '#F6465D'};
      this.Price = price;
    };
    this.price.error = error => {
      console.log(error);
    };

    this.spread.onmessage = event => {
      let stockObject = JSON.parse(event.data);
      let spread = (stockObject.data.a - stockObject.data.b) / stockObject.data.a * 100;
      this.spreadPrice = parseFloat(spread).toFixed(3);
    };
    this.spread.error = error => {
      console.log(error);
    };

  },
};
</script>

<style scoped lang="scss">
table {
  margin: 100px auto;
  overflow: hidden;
  width: 400px;
  color: #fff;
  border: 1px solid grey;
  background-color: rgb(22, 26, 30, 0.8);
}

th {
  padding: 10px;
  border: 1px solid grey;
}

tr {
  padding: 30px;
}

td {
  border: 1px solid grey;
  text-align: center;
}

.ask {
  color: rgb(246, 70, 93);
}

.bid {
  color: rgb(14, 203, 129);
}

.white {
  color: #fff
}
</style>
