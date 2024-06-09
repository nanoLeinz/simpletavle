<template>
  <div id="app">
    <h1>Harga Crypto</h1>
    <button class="btn btn-primary" @click="fetchData">Get Data</button>
    <table class="table table-striped mt-3">
      <thead>
        <tr>
          <th>Name</th>
          <th>Symbol</th>
          <th>Price USD</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="coin in coins" :key="coin.id">
          <td>{{ coin.name }}</td>
          <td>{{ coin.symbol }}</td>
          <td>{{ coin.price_usd }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      coins: [],
    };
  },
  methods: {
    fetchData() {
      axios
        .get("https://api.coinlore.net/api/tickers/")
        .then((response) => {
          this.coins = response.data.data;
        })
        .catch((error) => {
          console.error("Error fetching data:", error);
        });
    },
  },
};
</script>

<style>
#app {
  font-family: Arial;
  text-align: center;
  margin-top: 20px;
}

table {
  margin: 20px auto;
  width: 80%;
}
</style>
