<template>
  <div class="gn-input">
    <label
      v-if="config.label"
      class="label"
    >{{ config.label }}：</label>
    <el-input
      v-model="value"
      :type="config.type || 'text'"
      clearable
      :placeholder="config.placeholder || `请输入${config.label}`"
    >
    </el-input>
  </div>
</template>

<script>
export default {
  name: 'GnInput',
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
.gn-input {
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
