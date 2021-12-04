<template>
  <div class="page-wrap">
    <v-snackbar
      :timeout="4000"
      top
      right
      v-model="snackbar"
      class="notification"
    >
      <div class="action">
        Message sent
      </div>
      <v-btn
        text
        icon
        @click=""
      >
        <v-icon>mdi-close</v-icon>
      </v-btn>
    </v-snackbar>
    <hidden point="mdUp">
      <div class="logo logo-header">
        <nuxt-link :to="routeLink.lotus.home">
          <img :src="logo" alt="logo">
          <span class="use-text-title">
            {{ brand.lotus.projectName }}
          </span>
        </nuxt-link>
      </div>
    </hidden>
    <v-container class="inner-wrap max-md">
      <v-btn
        :href="routeLink.lotus.home"
        icon
        class="backtohome"
      >
        <i class="ion-ios-home-outline" />
        <i class="ion-ios-arrow-thin-left" />
      </v-btn>
      <div class="decoration">
        <svg class="left-deco">
          <use xlink:href="/images/lotus/deco-bg-left.svg#main" />
        </svg>
        <svg class="right-deco">
          <use xlink:href="/images/lotus/deco-bg-right.svg#main" />
        </svg>
      </div>
      <v-card class="form-box fragment-fadeUp">
        <div class="full-form-wrap">
          <h3 class="use-text-title title-contact pb-3 text-center">
            {{ $t('common.contact_title2') }}
          </h3>
          <h4 class="pb-3 text-center">
            [experimental]
          </h4>

          <h3 class="pb-3 text-center">
              Your daily lotus rewards: {{dailyRewards.toFixed(2)}} XPI
          </h3>
          <h3 class="pb-3 text-center">
              Daily electricity cost: {{electricityCosts.toFixed(2)}} usd
          </h3>

          <div class="form">
            <v-form
              ref="form"
              v-model="valid"
            >
              <v-row class="spacing6">
                <v-col cols="12" sm="16" class="px-9">
                  <v-select
                    return-object
                    ref='gpuSelect'
                    v-model="gpuSelected"
                    :items="items"
                    :item-text="'name'"
                    attach
                    class="input light"
                    label="GPU"
                    @change='updateHashrate'
                  ></v-select>
                </v-col>
                <v-col cols="12" sm="12" class="px-6">

                  <v-text-field
                    v-model="user_hashrate"
                    :label="$t('common.user_hashrate')"
                    color="white"
                    type="number"
                    suffix="mh/s"
                    class="input light"
                    filled
                    required
                  />
                </v-col>
                <v-col cols="12" sm="12" class="px-6">
                  <v-text-field
                    v-model="user_watt"
                    type="number"
                    :label="$t('common.user_power_consumption')"
                    class="input light"
                    color="white"
                    suffix="watt"
                    filled
                  />
                </v-col>
                <v-col cols="12" sm="12" class="px-6">
                  <v-text-field
                    v-model="user_watt_cost"
                    type="number"
                    :label="$t('common.watt_cost')"
                    color="white"
                    suffix="USD"
                    class="input light"
                    filled
                  />
                </v-col>

<!--
                <v-col cols="12" class="px-6">
                  <v-textarea
                    v-model="message"
                    rows="6"
                    color="white"
                    class="input light"
                    filled
                    :label="$t('common.form_message')"
                  />
                </v-col> -->
              </v-row>


              <div class="flex pb-3">
                <h3 class="pb-3">
                  Rewards:
                </h3>
                <v-data-table
                  :headers="headers_profitability"
                  :hide-default-footer="true"
                  :items="dataItems"
                  :items-per-page="5"
                  class="elevation-1 rewards_table"
                >
              </v-data-table>

              </div>

              <div class="flex pb-3">
                <h3 class="pb-3">
                  Electricity costs:
                </h3>
                <v-data-table
                  :headers="headers_electricity"
                  :hide-default-footer="true"
                  :items="dataElectricity"
                  :items-per-page="5"
                  class="elevation-1 rewards_table"
                ></v-data-table>

              </div>

              <div class="info_calculator">
                <p class="desc use-text-subtitle2 text-center">
                  {{ $t('common.contact_subtitle') }}
                </p>

                <p>Average Price: {{ format_to_X_decimals(avg_price, 5) }} USDT</p>
                <p>Current difficulty: {{ format_to_X_decimals(current_difficulty, 2) }}</p>
                <p>Total network hashrate: {{ format_to_X_decimals(total_network_hash_rate / 1000000000, 2)  }} GHs</p>
                ** decimal places rounded for readability, algo uses full values
                <br>
                ** values from exbitron and givelotus explorer apis.
              </div>
              <!-- <div class="btn-area flex">
                <div class="form-control-label">
                  <span>
                    <a href="#" class="link">
                    </a>
                  </span>
                </div>
                <v-btn
                  :block="isMobile"
                  color="secondary"
                  large
                >
                  {{ $t('common.update_data') }}
                </v-btn>
              </div> -->
            </v-form>
          </div>
        </div>
      </v-card>
    </v-container>
  </div>
</template>

<style lang="scss" scoped>
@import './form-style.scss';
@import '../Title/title-style.scss';
</style>

<script>
import logo from '~/static/images/logo.png'
import brand from '~/static/text/brand'
import link from '~/static/text/link'
import Hidden from '../Hidden'

export default {
  components: {
    Hidden
  },
  props: {
    avg_price: {
      type: String,
    },
    current_difficulty: {
      type: String,
    },
    total_network_hash_rate: {
      type: String,
    }
  },
  data() {
    return {
      items: [
        { name: 'Nvidia GeFore RTX3090', hashrate: 900, watt_consumption: 290},
        { name: 'Radeon Pro W5500', hashrate: 615, watt_consumption: 120},
        { name: 'Radeon RX 570 ', hashrate: 330, watt_consumption: 110},
        { name: 'AMD 6900 XT', hashrate: 2200, watt_consumption: 250},
        { name: 'AMD 6800 XT', hashrate: 2100, watt_consumption: 250},
        { name: 'AMD 6600 XT', hashrate: 1100, watt_consumption: 175},
        { name: 'Mac Mini M1', hashrate: 80, watt_consumption: 20},
        { name: 'other', hashrate: 0, watt_consumption: 0},
      ],
      gpuSelected: [],
      user_hashrate: 3800,
      user_watt: 700,
      user_watt_cost: 0.1,
      valid: true,
      snackbar: false,
      message: '',
      checkbox: false,
      logo: logo,
      brand: brand,
      routeLink: link,
      headers_profitability: [
        {
          text: 'timeframe',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Lotus', value: 'xpi' },
        { text: 'USDT', value: 'usdt' },
      ],
      headers_electricity: [
        {
          text: 'timeframe',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'kwh', value: 'kwh' },
        { text: 'USD', value: 'usd' },
      ],
      dataElectricity: [
        {
          name: 'Hourly',
          kwh: 150,
          usd: 6.0,
        },
        {
          name: 'Daily',
          kwh: 237,
          usd: 9.0,
        },
        {
          name: 'Weekly',
          kwh: 262,
          usd: 16.0,
        },
        {
          name: 'Monthly',
          kwh: 305,
          usd: 3.7,
        },
      ],
      dataItems: [
        {
          name: 'Hourly',
          xpi: 150,
          usdt: 6.0,
        },
        {
          name: 'Daily',
          xpi: 237,
          usdt: 9.0,
        },
        {
          name: 'Weekly',
          xpi: 262,
          usdt: 16.0,
        },
        {
          name: 'Monthly',
          xpi: 305,
          usdt: 3.7,
        },
      ],
      headers_other: [
        {
          text: 'timeframe',
          align: 'start',
          sortable: false,
          value: 'name',
        },
        { text: 'Lotus', value: 'xpi' },
        { text: 'USDT', value: 'usdt' },
      ],
      dataOther: [
        {
          name: 'Hourly',
          xpi: 150,
          usdt: 6.0,
        },
        {
          name: 'Daily',
          xpi: 237,
          usdt: 9.0,
        },
        {
          name: 'Weekly',
          xpi: 262,
          usdt: 16.0,
        },
        {
          name: 'Monthly',
          xpi: 305,
          usdt: 3.7,
        },
      ],
    }
  },
  methods: {
    validate() {
      if (this.$refs.form.validate()) {
        this.snackbar = true
      }
    },
    format_to_X_decimals(string, number_of_decimals) {
      let val = parseFloat(string)
      val = val.toFixed(number_of_decimals)

      return val
    },
    updateHashrate() {
      this.user_hashrate = this.gpuSelected.hashrate
      this.user_watt = this.gpuSelected.watt_consumption
    }
  },
  computed: {
    isMobile() {
      const smDown = this.$store.state.breakpoints.smDown
      return smDown.indexOf(this.$mq) > -1
    },
    dailyRewards() {
      // I have no idea how this works.
      let network_hashrate_gh = this.total_network_hash_rate / 1000000000
      let daily_xpi = (Math.log(this.current_difficulty/16,2)+1)*260/2*this.user_hashrate/1000/network_hashrate_gh*720
      let daily_usd = daily_xpi * this.avg_price

      //hourly
      this.dataItems[0].usdt = (daily_usd / 24).toFixed(2)
      this.dataItems[0].xpi = (daily_xpi / 24).toFixed(2)

      //daily
      this.dataItems[1].usdt = daily_usd.toFixed(2)
      this.dataItems[1].xpi = daily_xpi.toFixed(2)

      //weekly
      this.dataItems[2].usdt = (daily_usd * 7).toFixed(2)
      this.dataItems[2].xpi = (daily_xpi * 7).toFixed(2)

      //monthly
      this.dataItems[3].usdt = (daily_usd * 30).toFixed(2)
      this.dataItems[3].xpi = (daily_xpi * 30).toFixed(2)

      return daily_xpi
    },
    electricityCosts() {
      let daily_electricity_consumption = this.user_watt * 24 / 1000
      let hourly_electricity_consumption = daily_electricity_consumption / 24
      let weekly_electricity_consumption = daily_electricity_consumption * 7
      let monthly_electricity_consumption = daily_electricity_consumption * 30

      let daily_electricity_cost = daily_electricity_consumption * this.user_watt_cost
      let hourly_electricity_cost = hourly_electricity_consumption * this.user_watt_cost
      let weekly_electricity_cost = weekly_electricity_consumption * this.user_watt_cost
      let monthly_electricity_cost = monthly_electricity_consumption * this.user_watt_cost

      //hourly
      this.dataElectricity[0].kwh = hourly_electricity_consumption.toFixed(2)
      this.dataElectricity[0].usd = hourly_electricity_cost.toFixed(2)

      //daily
      this.dataElectricity[1].kwh = daily_electricity_consumption.toFixed(2)
      this.dataElectricity[1].usd = daily_electricity_cost.toFixed(2)

      //weekly
      this.dataElectricity[2].kwh = weekly_electricity_consumption.toFixed(2)
      this.dataElectricity[2].usd = weekly_electricity_cost.toFixed(2)

      //monthly
      this.dataElectricity[3].kwh = monthly_electricity_consumption.toFixed(2)
      this.dataElectricity[3].usd = monthly_electricity_cost.toFixed(2)

      return daily_electricity_cost
    }
  }
}
</script>
