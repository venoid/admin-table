<template>
<section class="table">
  <b-table
    :data="tableData"
    :hoverable="true"
    :loading="isLoading"
    :paginated="paginated"
    :pagination-simple="isPaginationSimple"
    backend-pagination
    pagination-size="is-small"
    :current-page="iCurrentPage"
    :per-page="iPerPage"
    :total="total"
    @page-change="emitPaginationChange"

    :backend-sorting="backendSorting"
    :default-sort="defaultSort"
    @sort="emitSortEvent"

  >
    <template slot-scope="props">
      <b-table-column
        v-for="(column, index) in tableColumns"
        :key="index"
        :label="column.label"
        :width="column.width"
        :field="column.fieldName"
        :numeric="column.type === 'id'"
        :sortable="column.sortable || false"
      >
        <div v-if="column.type === 'action'" class="buttons">
          <b-button
            v-for="(action, i) in column.actions"
            :key="`button.${i}`"
            type="is-primary"
            size="is-small"
            outlined
            @click="action.callback(props.row)"
          >
            <b-icon
              :icon="action.icon || 'help-circle'"
              size="is-small"
            ></b-icon>
          </b-button>
        </div>
        <div v-else>
          {{ column.field(props.row) }}
        </div>
      </b-table-column>
    </template>

    <template slot="empty">
      <section class="section">
        <div class="content has-text-grey has-text-centered">
          <p v-if="errorMessage">{{ errorMessage }}</p>
        </div>
      </section>
    </template>
  </b-table>
  <b-select v-if="paginated" class="per-page" size="is-small" v-model="iPerPage" @input="savePerPage">
        <option v-for="(option, index) in perPageOptions" :key="`perpage${index}`" :value="option.value">{{ option.label }}</option>
  </b-select>
</section>
</template>

<script>
import md5 from 'md5'

export default {
  name: 'venoid-table',
  props: {
    tableColumns: {
      type: Array,
      default() {
        return undefined
      }
    },
    tableData: {
        type: Array,
        default() {
            return undefined
        }
    },
    isLoading: {
        type: Boolean,
        default: false
    },
    paginated: {
      type: Boolean,
      default: false
    },
    isPaginationSimple: {
      type: Boolean,
      default: false
    },
    totalDataCount: {
      type: Number,
      default: null
    },
    currentPage: {
      type: Number,
      default: 1
    },
    perPageOptions: {
      type: Array,
      default() {
        return [
          {
            value: 5,
            label: '5'
          },
          {
            value: 10,
            label: '10'
          },
          {
            value: 25,
            label: '25'
          },
          {
            value: 50,
            label: '50'
          },
          {
            value: 100,
            label: '100'
          }
        ]
      }
    },
    defaultSort: {
      type: Array,
      default() {
        return []
      }
    },
    backendSorting: {
      type: Boolean,
      default: false
    },
    errorMessage: null
  },
  mounted() {
    if (process.browser) {
      this.iPerPage = parseInt(localStorage.getItem(this.getPerPageKey())) || 5
      if(this.paginated) {
        this.emitPaginationChange()
      }
    }
  },
  data() {
    return {
      iPerPage: 5,
      perPageLocalStorageKey: null,
      iCurrentPage: this.currentPage,
      sortField: 'title',
      sortOrder: 'desc',
    }
  },
  computed: {
    total() {
      if (this.totalDataCount === null) {
        if (this.tableData) {
          return this.tableData.length
        }
      }
      return this.totalDataCount
    }
  },
  methods: {
    savePerPage(value) {
      this.emitPaginationChange()
      if (process.browser) {
        localStorage.setItem(this.getPerPageKey(), value)
      }
    },
    getPerPageKey() {
      return `per-page: ${md5(JSON.stringify(this.tableColumns))}`
    },
    emitPaginationChange(d) {
      this.iCurrentPage = d || 1
      this.$emit('pagination-change', {
        currentPage: this.iCurrentPage,
        perPage: this.iPerPage
      })
    },
    emitSortEvent(field, order) {
      this.sortField = field
      this.sortOrder = order
      this.$emit('sort', {
        field,
        order
      })
    }
  }
}
</script>

<style scoped>
  .table {
    position: relative;
  }
  .per-page {
    position: absolute;
    bottom: 1.5rem;
  }
</style>
