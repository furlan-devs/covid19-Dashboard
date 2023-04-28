<template>
  <div class="table-container">
    <!-- Cabeçalho da tabela -->
    <div class="header-row">
      <div class="column" v-for="column in columns" :key="column">
        {{ column }}
      </div>
    </div>
    <!-- Linha de dados -->
    <div v-if="filteredData.length === 0" class="data-row">
      <div class="column" :colspan="columns.length">
        Não há dados disponíveis.
      </div>
    </div>
    <div v-else v-for="data in formattedData" :key="data.Date" class="data-row">
      <div class="column">{{ data.Date }}</div>
      <div class="column">{{ data.Confirmed }}</div>
      <div class="column">{{ data.Deaths }}</div> 
      <div class="column">{{ data.Recovered }}</div>
    </div>
    <!-- Total de dados -->
    <div class="data-row total-row">
      <div class="column">{{ totalLabel }}</div>
      <div class="column">{{ totalConfirmed }}</div>
      <div class="column">{{ totalDeaths }}</div>
      <div class="column">{{ totalRecovered }}</div>
    </div>
  </div>
</template>

<script>
import moment from 'moment';
import 'moment/locale/pt-br';

export default {
  props: {
    filteredData: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      columns: ['Data', 'Casos confirmados', 'Mortes', 'Recuperados'],
      totalLabel: 'Total'
    };
  },
  computed: {
    formattedData() {
      return this.filteredData.map(data => ({
        ...data,
        Date: moment.utc(data.Date).local().format('DD/MM/YYYY')
      }));
    },
    totalConfirmed() {
      return this.sumBy('Confirmed');
    },
    totalDeaths() {
      return this.sumBy('Deaths');
    },
    totalRecovered() {
      return this.sumBy('Recovered');
    }
  },
  methods: {
    sumBy(key) {
      return this.filteredData.reduce((total, data) => total + data[key], 0);
    }
  }
}
</script>
<style>
.table-container {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.3);
  overflow: auto;
  color: #000;
  width: 100%; 
  min-height: 84.6%;
  max-height: 84.6%; 
}


.table-container::-webkit-scrollbar {
  width: 10px;
  background-color: #f5f5f5;
}

.table-container::-webkit-scrollbar-thumb {
  background-color: #c0c0c0;
  border-radius: 10px;
}

.table-container::-webkit-scrollbar-thumb:hover {
  background-color: #a0a0a0;
}


.header-row, .data-row {
  display: flex;
}

.header-row {
  background-color: #f5f5f5;
  font-weight: bold;
  position: sticky;
  top: 0;
  z-index: 1;
}

.header-row .column {
  height: 50px; /* altura original */
  display: flex;
  justify-content: center;
  align-items: center;
}

.data-row {
  border-top: 1px solid #ddd;
}

.data-row:last-child {
font-weight: bold;
position: sticky;
bottom: 0;
background-color: white;
  border-bottom: 1px solid #ddd;
}

.column {
  flex: 1;
  padding: 5px; 
  text-align: center;
  border-left: 1px solid #ddd;
}

.column:first-child {
  border-left: none;
}
</style>
