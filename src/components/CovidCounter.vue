<template>
  <div class="counter-wrapper">
    <h1 class="date">Updated: {{ currentDate }}</h1>
    <div class="counters">
      <div class="counter confirmed" :style="{ backgroundColor: confirmedColor }">
        <h2>Confirmed Cases</h2>
        <p>{{ confirmed }}</p>
      </div>
      <div class="counter deaths" :style="{ backgroundColor: deathsColor }">
        <h2>Deaths</h2>
        <p>{{ deaths }}</p>
      </div>
      <div class="counter recovered" :style="{ backgroundColor: recoveredColor }">
        <h2>Recovered</h2>
        <p>{{ recovered }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      confirmed: 0,
      deaths: 0,
      recovered: 0,
      confirmedColor: '',
      deathsColor: '',
      recoveredColor: '',
      currentDate: '',
    };
  },

  created() {
    this.fetchData();
  },

  methods: {
    async fetchData() {
      const { data } = await axios.get('https://api.covid19api.com/summary');
      this.confirmed = data.Global.TotalConfirmed;
      this.deaths = data.Global.TotalDeaths;
      this.recovered = data.Global.TotalRecovered;
      this.currentDate = new Date(data.Date).toLocaleDateString();
      console.log(this.deaths, data.Global.TotalDeaths)

      this.setColor(this.deaths, data.Global.NewDeaths, 'deathsColor');
      this.setColor(this.confirmed, data.Global.NewConfirmed, 'confirmedColor');
      this.setColor(this.recovered, data.Global.NewRecovered, 'recoveredColor');
    },

    setColor(current, newCount, colorType) {
      console.log(current, newCount, "este")

      if (current < newCount) {
        this[colorType] = 'red';
      } else if (current === newCount) {
        this[colorType] = 'blue';
      } else {
        this[colorType] = 'green';
      }
    },
  },
};
</script>

<style scoped>
.counter-wrapper {
  width: 45vw;
  height: 39vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 1rem;
  margin: 0 auto;
}

.counters {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

.counters h2{
  font-size: 1.2rem;
}

.counters p{
  font-size: 2.5rem;
  font-weight: bold;
}

.counter {
  width: 16rem;
  height: 13rem;
  padding: 1rem;
  border-radius: 10px;
  color: white;
  text-align: center;
  justify-content: center;
  display: flex;
  flex-direction: column;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.3);
}

.confirmed {
  background-color: #f6c23e;
}

.deaths {
  background-color: #e74a3b;
}

.recovered {
  background-color: #1cc88a;
}

.date {
  font-size: 1.5rem;
  color: #000;
  margin-bottom: 2rem;
}
</style>
