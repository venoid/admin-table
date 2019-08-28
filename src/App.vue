<template>
  <div id="app">
    <h1>Venoid table</h1>
    <div class="example-container">
      <venoid-table
        :table-columns="tableColumns"
        :table-data="tableData"
        :isLoading="isLoading"
      />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import VenoidTable from './venoid-table.vue';

export default {
  name: 'app',
  components: {
    VenoidTable,
  },
  data() {
    return {
      tableColumns: [
        {
          type: 'id',
          field: (r) => r.id,
          label: 'ID',
          width: '20'
        },
        {
          type: 'string',
          label: 'Title',
          field: (r) => r.title,
          width: '60'
        },
        {
          type: 'number',
          label: 'Author Id',
          field: (r) => r.author_id,
          width: '60'
        },
        {
          type: 'number',
          label: 'Pages',
          field: (r) => r.pages,
          width: '60'
        },
        {
          type: 'string',
          label: 'Release Date',
          field: (r) => r.releaseDate,
          width: '60'
        },
        {
          type: 'string',
          label: 'ISBN',
          field: (r) => r.isbn,
          width: '60'
        },
        {
          type: 'action',
          label: 'Actions',
          width: '5',
          actions: [
            {
              callback: (rowData) => {
                this.test(rowData)
              },
              icon: 'pencil'
            }
          ]
        }
      ],
      tableData: [],
      isLoading: false
    }
  },
  async created() {
    this.isLoading = true
    const {data} = await axios.get('https://my-json-server.typicode.com/dmitrijt9/book-api-mock/books')
    this.tableData = data
    this.isLoading = false
  },
  methods: {
    test(data) {
      window.confirm(`${data.title}`)
    }
  }
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.example-container {
  padding-top: 16px;
  margin: auto;
  max-width: 80%;
}
</style>
