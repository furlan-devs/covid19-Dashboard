<template>
  <Header title="Dashboard" />
  <div class="dashboard">
<div class="filters-container">
</div>

<div class="main-section">
  <div class="top-left-column">
    <CovidCounter />
  </div>

  <div class="top-right-column">
    <LastTenDaysData country-slug="brazil" />
  </div>

  <div class="bottom-left-column">
    <Filter @filter-data="fetchData"></Filter>
    <Data :filteredData="filteredData"></Data>
  </div>

  <div class="bottom-right-column">
    <Map></Map>
  </div>

</div>
</div>
</template>
<script>
import Header from '../components/Header.vue'
import Filter from '../components/Filter.vue'
import Data from '../components/Data.vue'
import CovidCounter  from '../components/CovidCounter.vue'
import LastTenDaysData   from '../components/LastTenDaysData.vue'
import Map   from '../components/Map.vue'

export default {
  name: "Dashboard",
  components: {
    Header,
    Filter,
    Data,
    CovidCounter,
    LastTenDaysData,
    Map
  },
  data() {
    return {
      filteredData: []
    }
  },
  methods: {
    fetchData(filter) {
      const apiUrl = `https://api.covid19api.com/country/${filter.country}?from=${filter.from}&to=${filter.to}`
      fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
          this.filteredData = data
        })
    }
  }
};
</script>
<style>
.dashboard {
  display: flex;
  flex-direction: column;
  height: calc(100vh - 5.75rem);
  width: calc(100vw - 5rem);
  margin: 0 auto;
}

.filters-container {
  padding: 16px;
  margin: 0 auto;

}

.main-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
  gap: 16px;
}

.top-left-column {
  grid-column: 1 / 2;
  grid-row: 1 / 2;
  width: 100%; 
  height: 39vh; 

}

.top-right-column {
  grid-column: 2 / 3;
  grid-row: 1 / 2;
  width: 100%; 
  height: 39vh; 
  border: 1px solid lightgray;
  border-radius: 10px;
  background-color: lightgray;


  
}

.bottom-left-column {
  grid-column: 1 / 2;
  grid-row: 2 / 3;
  width: 100%; 
  height: 39vh; 

}

.bottom-right-column {
  grid-column: 2 / 3;
  grid-row: 2 / 3;
  width: 100%; 
  height: 39vh; 
  border: 1px solid lightgray;
  background-color: lightcyan;
  border-radius: 10px;

}

</style>