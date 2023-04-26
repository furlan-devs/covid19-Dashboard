<template>
    <Header title="Dashboard"/>

  <div class="dashboard">

    <div class="filters-container">
      <Filter @filter-data="fetchData"></Filter>
    </div>

    <div class="main-section">
      <div class="left-column">
        <Data :filteredData="filteredData"></Data>
      </div>

      <div class="right-column">
        <!-- Adicione conteúdo para a coluna direita aqui -->
      </div>

      <div class="bottom-row">
        <!-- Adicione conteúdo para a linha inferior aqui -->
      </div>
    </div>
  </div>
</template>

<script>
import Header from '../components/Header.vue'
import Filter from '../components/Filter.vue'
import Data from '../components/Data.vue'

export default {
  name: "Dashboard",
  components: {
    Header,
    Filter,
    Data
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
  background-color: gray;

}

.filters-container {
  padding: 16px;
  background-color: lightpink;
  margin: 0 auto;

}

.main-section {
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: auto auto 1fr;
}

.left-column {
  
  grid-column: 1 / 2;
  width: 45vw; 
  height: 39vh; 
  /* overflow: auto;  */
  margin-left: auto;
}

.right-column {
  grid-column: 2 / 3;
  background-color: lightblue;
  width: 45vw; 
  height: 39vh; 
  
}

.bottom-row {
  margin: 0 auto;
  grid-column: 1 / -1;
  grid-row: 3 / 4;
  background-color: lightgreen;
  width: 90vw; 
  height: 38vh; 

}

.left-column,
.right-column,
.bottom-row {
  padding: 16px;
  border: 1px solid #ccc;
}
</style>
