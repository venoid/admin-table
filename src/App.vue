<template>
  <div id="app">
    <h1>Venoid table</h1>
    <a href="https://github.com/venoid/admin-table#readme">
      <b-icon icon="link" />
      DOCS
    </a>
    <hr>
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
          fieldName: 'id',
          field: (r) => r.id,
          label: 'ID',
          width: '20'
        },
        {
          type: 'string',
          label: 'Title',
          fieldName: 'title',
          field: (r) => r.title,
          width: '60',
          sortable: true
        },
        {
          type: 'number',
          label: 'Author Id',
          fieldName: 'author_id',
          field: (r) => r.author_id,
          width: '60'
        },
        {
          type: 'number',
          label: 'Pages',
          fieldName: 'pages',
          field: (r) => r.pages,
          width: '60'
        },
        {
          type: 'string',
          label: 'Release Date',
          fieldName: 'releaseDate',
          field: (r) => r.releaseDate,
          width: '60'
        },
        {
          type: 'string',
          label: 'ISBN',
          fieldName: 'isbn',
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
    const vm = this
    var oReq = new XMLHttpRequest();
    oReq.onreadystatechange = function() {
      if (this.readyState == 4 && this.status == 200) {
        vm.tableData = JSON.parse(this.responseText)
        vm.isLoading = false
      }
    }
    oReq.open("GET", "https://my-json-server.typicode.com/dmitrijt9/book-api-mock/books");
    oReq.send();
  },
  methods: {
    test(data) {
      console.log(data)
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
