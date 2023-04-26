<template>
  <div>
    <Filter @filter-data="fetchData"></Filter>
    <Data :filteredData="filteredData"></Data>
  </div>
</template>

<script>
import Filter from './Filter.vue'
import Data from './Data.vue'

export default {
  components: {
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
}
</script>


