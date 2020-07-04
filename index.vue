<template>
  <div class="search-form-pagination">
    <div
      v-if="componentImstances.length > 0"
      class="search-form"
    >
      <component
        :is="item.imstance"
        v-for="(item, i) in componentImstances"
        :key="i"
        :config="item"
        @change="change"
      />
      <el-button
        type="primary"
        @click="onSearch"
      >{{ searchBtnText }}</el-button>
    </div>
    <div class="table">
      <slot name="table"></slot>
    </div>
    <div class="pagination">
      <Pagination
        :current-page="currentPage"
        :page="currentPage"
        :limit="pageSize"
        :total="total"
        @pagination="paginationChange"
      ></Pagination>
    </div>
  </div>
</template>

<script>
import Pagination from '@/components/Pagination';
import { deepClone as $deepClone } from '@/utils/deepClone';

export default {
  name: 'SearchBar',
  components: {
    Pagination
  },
  props: {
    config: {
      type: Array,
      default() {
        return [];
      }
    },
    total: { // 总条目数
      type: Number,
      required: true,
      default: 1
    },
    searchBtnText: {
      type: String,
      default: '查询'
    },
    loadTrigger: { // 值为true时，挂载完触发onSearch通知父组件
      type: Boolean,
      default: true
    },
  },
  data() {
    return {
      searchFormConfig: [],
      searchParam: {},
      currentPage: 1,
      pageSize: 10,
    };
  },
  computed: {
    componentImstances() {
      const { searchFormConfig } = this;
      return searchFormConfig.map((item, i) => {
        try {
          item.imstance = resolve => require([`./components/${item.name}.vue`], resolve);
          item.index = i;
        } catch (e) {
          console.log(e);
        }
        return item;
      });
    }
  },
  watch: {
    config(newValue) {
      this.init();
    },
  },
  created() {
    this.init();
  },
  mounted() {
    this.loadTrigger && this.onSearch();
  },
  methods: {
    init() {
      const { config } = this;
      this.searchFormConfig = $deepClone(config);
      for (const item of config) {
        this.setSearchParam(item.key, item.value);
      }
    },
    onSearch() {
      const { pageSize, currentPage, searchParam } = this;
      this.$emit('onSearch', { page: currentPage, per_page: pageSize, ...searchParam });
    },
    searchChange() {
      const { pageSize, currentPage, searchParam } = this;
      this.$emit('change', { page: currentPage, per_page: pageSize, ...searchParam });
    },
    change(index, value) {
      const item = this.searchFormConfig[index];
      item.value = value;
      this.setSearchParam(item.key, value);
      this.searchChange();
    },
    setSearchParam(key, value) {
      this.searchParam[key] = value || '';
    },
    paginationChange(current) {
      this.pageSize = current.limit;
      this.currentPage = current.page;
      this.onSearch();
    }
  }
};

</script>

<style lang="scss" scoped>
.search-form-pagination {
  .search-form {
    display: flex;
    flex-wrap: wrap;
  }

  .table {
    width: 100%;
    min-height: 100px;
    margin: 20px 0;
  }
  .pagination {
    /deep/.el-pagination {
      display: flex;
      justify-content: center;
    }
  }
}
</style>
