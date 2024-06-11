<script>
import '@ag-grid-community/styles/ag-grid.css'
import '@ag-grid-community/styles/ag-theme-quartz.css'
import { AgGridVue } from 'ag-grid-vue3'
import { ref } from 'vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    AgGridVue
  },
  setup() {
    const items = ref([]);

    const fetchData = async () => {
      try {
        const response = await axios.get('https://api.coindesk.com/v1/bpi/currentprice.json');
        items.value = response.data;
      } catch (error) {
        console.error('Error fetching data:', error);
      } finally {
        console.log(JSON.stringify(items.value, undefined, 4));
      }
    };

    return {
      fetchData,
      columnDefs: [
        { headerName: 'Make', field: 'make' },
        { headerName: 'Model', field: 'model' },
        { headerName: 'Price', field: 'price' }
      ],
      rowData: [
        { make: 'Toyota', model: 'Celica', price: 35000 },
        { make: 'Ford', model: 'Mondeo', price: 32000 },
        { make: 'Porsche', model: 'Boxster', price: 72000 }
      ]
    }
  }
}
</script>

<template>
    <br>
    <hr>
    <button @click="fetchData">Fetch Data</button>
    <br>
    <ag-grid-vue
      style="width: 500px; height: 200px"
      class="ag-theme-quartz"
      :columnDefs="columnDefs"
      :rowData="rowData"
    >
    </ag-grid-vue>
</template>