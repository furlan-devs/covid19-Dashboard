<template>
  <div>
    <h1>Dashboard Covid-19</h1>
    <table>
      <thead>
        <tr>
          <th>Data</th>
          <th>País</th>
          <th>Novos Casos</th>
          <th>Total de Casos</th>
          <th>Novas Mortes</th>
          <th>Total de Mortes</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="country in countries" :key="country.Date + country.Country">
          <td>{{ country.Date }}</td>
          <td>{{ country.Country }}</td>
          <td>{{ country.NewConfirmed }}</td>
          <td>{{ country.TotalConfirmed }}</td>
          <td>{{ country.NewDeaths }}</td>
          <td>{{ country.TotalDeaths }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Dashboard',
  data() {
    return {
      countries: []
    }
  },
  created() {
    axios
      .get('https://api.covid19api.com/summary')
      .then(response => {
        this.countries = response.data.Countries
      })
      .catch(error => {
        console.log(error)
      })
  }
}
</script>

<style>
table {
  border-collapse: collapse;
  width: 100%;
}

th, td {
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}
</style>
