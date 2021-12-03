<template>
  <div>
    <Calculator
      :avg_price="avg_price"
      :current_difficulty="current_difficulty"
      :total_network_hash_rate="total_network_hash_rate"
     />
  </div>
</template>

<script>
import Calculator from '~/components/Forms/Calculator'
import brand from '~/static/text/brand'

export default {
  components: {
    Calculator
  },
  async asyncData({ params, $axios }) {
    // We can use async/await ES6 feature
    const res1 = await $axios.get(
      "https://www.exbitron.com/api/v2/peatio/public/markets/xpiusdt/tickers"
    );
    const res2 = await $axios.get(
      "https://explorer.givelotus.org/api/getdifficulty"
    );
    const res3 = await $axios.get(
      "https://explorer.givelotus.org/api/getnetworkhashps"
    );
    return {
          avg_price: res1.data.ticker.avg_price,
          current_difficulty: res2.data,
          total_network_hash_rate: res3.data };
  },
  head() {
    return {
      title: brand.lotus.name + ' - Calculator'
    }
  }
}
</script>
