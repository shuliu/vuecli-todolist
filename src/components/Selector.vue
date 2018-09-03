<template>
  <div class="select">
    <select v-model="selectIndex" >
      <option v-for="(item, key) in options" :key="key" :value="key">{{item.name}}</option>
    </select>

    <span v-if="showInfo()">{{selectIndex}}, {{selectName}}</span>
  </div>
</template>

<script>
export default {
  props: {
    list: {
      type: Array,
      default: function() { return []; }
    },
    value: Number
  },
  data() {
    return {
      options: this.list,
      selectIndex: this.value,
      selectName: ''
    }
  },
  created() {
    this.selectName = this.options.length > 0 ? this.options[0].name : this.selectName;
  },
  computed: {
  },
  methods: {
    showInfo() {
      return this.selectName !== '';
    },
    getSelectName() {
      this.selectName = this.options.length > 0 ? this.options[this.selectIndex].name : '';
    },
    emitSelectIndex() {
      this.$emit('selectIndex', this.selectIndex);
    },
    updateOptions() {
      this.options = this.list;
    },
    resetIndex() {
      this.selectIndex = 0;
    }
  },
  watch: {
    selectIndex: ['getSelectName', 'emitSelectIndex'],
    list: ['updateOptions', 'resetIndex'],
  }
}
</script>

<style>

</style>
