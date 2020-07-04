<template>
  <div class="gn-select">
    <label
      v-if="config.label"
      class="label"
    >{{ config.label }}：</label>
    <el-select
      v-model="value"
      :clearable="config.clearable || true"
      :placeholder="config.placeholder || `请选择${config.label}`"
    >
      <el-option
        v-for="(item, i) in config.options"
        :key="i"
        :label="item.label"
        :value="item.value"
      >
      </el-option>
    </el-select>
  </div>
</template>

<script>
export default {
  name: 'GnSelect',
  props: {
    config: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      value: ''
    };
  },
  watch: {
    value(newValue) {
      this.$emit('change', this.config.index, newValue);
    },
  },
  created() {
    this.init();
  },
  methods: {
    init() {
      this.value = this.config.value || '';
    }
  }
};
</script>
<style lang="scss" scoped>
.gn-select {
  display: inline-block;
  margin: 5px 10px;
  .label {
    width: 5em;
    font-weight: 400;
    white-space: nowrap;
  }
  /deep/.el-select {
    width: 200px;
  }
}
</style>
