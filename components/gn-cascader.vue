<template>
  <div class="gn-select">
    <label
      v-if="config.label"
      class="label"
    >{{ config.label }}：</label>
    <el-cascader
      v-model="value"
      :clearable="config.clearable || true"
      :options="config.options"
      :placeholder="config.placeholder || `请选择${config.label}`"
    />
  </div>
</template>

<script>
export default {
  name: 'GnCascader',
  props: {
    config: {
      type: Object,
      required: true
    },
  },
  data() {
    return {
      value: []
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
