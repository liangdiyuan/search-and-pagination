<template>
  <div class="gn-date-picker">
    <label
      v-if="config.label"
      class="label"
    >{{ config.label }}：</label>
    <el-date-picker
      v-model="value"
      :type="config.type"
      :format="config.format"
      :value-format="config.valueFormat || 'yyyyMMdd'"
      :placeholder="config.placeholder || `请选择${config.label}`"
    >
    </el-date-picker>
  </div>
</template>

<script>
export default {
  name: 'GnDatePicker',
  props: {
    config: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      value: ''
    };
  },
  watch: {
    value(newValue) {
      this.$emit('change', this.config.index, newValue);
    }
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
.gn-date-picker {
  display: inline-block;
  margin: 5px 10px;
  .label {
    width: 5em;
    font-weight: 400;
    white-space: nowrap;
  }
  /deep/.el-input {
    width: 200px;
  }
}
</style>
