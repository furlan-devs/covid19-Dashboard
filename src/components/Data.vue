<template>
    <div>
      <table>
        <thead>
          <tr>
            <th>Data</th>
            <th>Casos confirmados</th>
            <th>Mortes</th>
            <th>recuperados</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in filteredData" :key="data.Date">
            <td>{{ data.Date }}</td>
            <td>{{ data.Confirmed }}</td>
            <td>{{ data.Deaths }}</td>
            <td>{{ data.Recovered }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      filteredData: {
        type: Array,
        required: true
      }
    }
  }
  </script>

casos confirmados - Confirmed
Mortes do dia - Deaths
recuperados do dia - Recorved