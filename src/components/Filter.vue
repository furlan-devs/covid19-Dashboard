<template>
    <div class='filter-container'>
      <label>País:</label>
      <select v-model="selectedCountry">
        <option v-for="country in countries" :value="country.Slug" :key="country.Slug">{{ country.Country }}</option>
      </select>
      <label>De:</label>
      <input type="date" v-model="fromDate">
      <label>Para:</label>
      <input type="date" v-model="toDate">
      <button @click="filterData">Filtrar</button>
    </div>
  </template>
  
  <script>
  import axios from 'axios'
  export default {
    data() {
      return {
        selectedCountry: '',
        fromDate: '',
        toDate: '',
        countries: []
      }
    },
    mounted() {
      this.fetchCountries()
    },
    methods: {
      fetchCountries() {
        axios.get('https://api.covid19api.com/countries')
        .then(response => {
          this.countries = response.data
        })
        .catch(error => {
          console.error(error)
        })
},
filterData() {
        this.$emit('filter-data', {
          country: this.selectedCountry,
          from: this.fromDate + 'T00:00:00Z',
          to: this.toDate + 'T00:00:00Z'
        })
      }
    }
  }
  </script>

<style>
.filter-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px 20px 20px;
  border-radius: 10px;
}

label {
  margin-right: 0.5rem;
  color: #000;
}

select, input[type="date"] {
  margin-right: 2rem;
  padding: 0.5rem;
  border: 1px solid #bbb;
  background-color: #fff;
  color: #000;
  outline: none;
  border-radius: 10px;
}

select::-webkit-scrollbar {
  width: 10px;
  background-color: #f5f5f5;
}

select::-webkit-scrollbar-thumb {
  background-color: #c0c0c0;
  border-radius: 10px;
}

select::-webkit-scrollbar-thumb:hover {
  background-color: #a0a0a0;
}

input[type="date"]::-webkit-calendar-picker-indicator {
  filter: invert(1);
}

button {
  background-color: #007bff;
  color: #fff;
  padding: 0.636rem 1rem;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}


</style>