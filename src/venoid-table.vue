<template>
<section class="table">
  <b-table
    :data="tableData"
    :hoverable="true"
    :loading="isLoading"
    :paginated="paginated"
    :current-page="currentPage"
    :per-page="perPage"
    backend-pagination
    :total="total"
    @page-change="(page) => $emit('page-change', page)"
    pagination-size="is-small"
  >
    <template slot-scope="props">
      <b-table-column
        v-for="(column, index) in tableColumns"
        :key="index"
        :label="column.label"
        :width="column.width"
        :numeric="column.type === 'id'"
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
          <p>
            <b-icon icon="emoticon-sad" size="is-large"> </b-icon>
          </p>
          <p>Nothing here.</p>
          <p v-if="errorMessage">{{ errorMessage }}</p>
        </div>
      </section>
    </template>
  </b-table>
  <b-select v-if="paginated" class="per-page" size="is-small" v-model="perPage" @input="savePerPage">
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
            value: '5',
            label: 5
          },
          {
            value: '10',
            label: 10
          },
          {
            value: '15',
            label: 15
          },
          {
            value: '20',
            label: 20
          }
        ]
      }
    },
    errorMessage: null
  },
  data() {
    return {
      perPage: localStorage.getItem(this.getPerPageKey()) || 5,
      perPageLocalStorageKey: null
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
      localStorage.setItem(this.getPerPageKey(), value)
    },
    getPerPageKey() {
      return `per-page: ${md5(JSON.stringify(this.tableColumns))}`
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
