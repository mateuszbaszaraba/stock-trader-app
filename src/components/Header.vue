<template>
    <nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <router-link to="/" class="navbar-brand">Stock Trader</router-link>
    </div>

    <div class="collapse navbar-collapse">
      <ul class="nav navbar-nav">
        <router-link to="/portfolio" tag="li" activeClass="active"><a>Portfolio</a></router-link>
        <router-link to="/stocks" tag="li" activeClass="active"><a>Stocks</a></router-link>
      </ul>
      <strong class="navbar-text navbar-right">Funds: {{ funds | currency }}</strong>
      <ul class="nav navbar-nav navbar-right">
        <li><a href="#" @click="endDay">Next Day</a></li>
        <li class="dropdown" :class="{ open: isDropdownOpen }" @click="isDropdownOpen = !isDropdownOpen">
          <a 
            href="#" 
            class="dropdown-toggle" 
            data-toggle="dropdown" 
            role="button" 
            aria-haspopup="true" 
            aria-expanded="false">Save & Load <span class="caret"></span></a>
          <ul class="dropdown-menu">
            <li><a href="#" @click="saveData">Save data</a></li>
            <li><a href="#">Load data</a></li>
          </ul>
        </li>
      </ul>
    </div><!-- /.navbar-collapse -->
  </div><!-- /.container-fluid -->
</nav>
</template>

<script>
import {mapActions} from 'vuex';

export default {
  computed: {
    funds() {
      return this.$store.getters.funds
    }
  },
  methods: {
    ...mapActions([
      'randomizeStocks'
    ]),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks
      };
      this.$http.put('data.json', data);
    }
  },
  data() {
    return {
      isDropdownOpen: false
    }
  }
}
</script>