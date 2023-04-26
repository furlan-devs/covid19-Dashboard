<template>
  <div class="table-container">
    <div class="header-row">
      <div class="column">Data</div>
      <div class="column">Casos confirmados</div>
      <div class="column">Mortes</div>
      <div class="column">Recuperados</div>
    </div>
    <div v-if="filteredData.length === 0" class="data-row">
      <div class="column" colspan="4">Não há dados disponíveis.</div>
    </div>
    <div v-for="data in formattedData" :key="data.Date" class="data-row">
    <div class="column">{{ data.Date }}</div>
    <div class="column">{{ data.Confirmed }}</div>
    <div class="column">{{ data.Deaths }}</div>
    <div class="column">{{ data.Recovered }}</div>
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
  computed: {
  formattedData() {
    return this.filteredData.map(data => ({
      ...data,
      Date: moment.utc(data.Date).local().format('DD/MM/YYYY')
    }));
  }
}
}
</script>

<style>
.table-container {
  background-color: #fff;
  border-radius: 10px;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
  overflow: auto;
  color: #000;
  width: 100%; 
  height: 100%; 
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

.column {
  flex: 1;
  padding: 5px; /* Alterado de 10px para 5px */
  text-align: center;
  border-left: 1px solid #ddd;
}

.column:first-child {
  border-left: none;
}
</style>
